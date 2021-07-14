<template>
  <Header :totalIncome="state.totalIncome" />
  <Form @add-income="AddIncome" />
</template>

<script>
import { reactive, computed } from "vue";
import Header from "./components/Header.vue";
import Form from "./components/Form.vue";

export default {
  name: "App",
  components: {
    Header,
    Form,
  },
  setup() {
    const state = reactive({
      income: [],
      totalIncome: computed(() => {
        let temp = 0;
        if (state.income.length > 0) {
          for (let i = 0; i < state.income.length; i++) {
            temp += state.income[i].value;
          }
        }

        return temp;
      }),
    });

    function AddIncome(data) {
      let d = data.date.split("-");
      let newD = new Date(d[0], d[1], d[2]);

      state.income = [
        ...state.income,
        {
          id: Date.now(),
          desc: data.desc,
          value: parseInt(data.value),
          date: newD.getTime(),
        },
      ];
      console.log(state.income);
    }

    return { state, AddIncome };
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
}

body {
  background: #eee;
}
</style>
