<template>
  <v-app>
    <v-app-bar app color="teal" dark>
      <div class="d-flex align-center">
        <h3>Budgeter</h3>
      </div>
    </v-app-bar>
    <v-main class="mt-5">
      <MonthlyIncome
        :monthlyAmount="this.monthlyIncome"
        @income-submit="updateIncome"
      />
      <Expenses
        :expenses="this.monthlyExpenses"
        @expenses-submit="addExpense"
      />
      <IncomeCard :monthlyNet="this.monthlyNet" />
    </v-main>
  </v-app>
</template>

<script>
import MonthlyIncome from "./components/MonthlyIncome";
import Expenses from "./components/Expenses";
import IncomeCard from "./components/IncomeCard";

export default {
  components: {
    MonthlyIncome,
    Expenses,
    IncomeCard,
  },

  data() {
    return {
      monthlyIncome: 0,
      monthlyExpenses: [],
    };
  },
  methods: {
    addExpense(newExpense) {
      this.monthlyExpenses.push(newExpense);
      localStorage.setItem(
        "monthlyExpenses",
        JSON.stringify(this.monthlyExpenses)
      );
    },
    updateIncome(newIncome) {
      this.monthlyIncome = newIncome;
    },
  },
  computed: {
    totalMonthlyExpenses: function () {
      let total = 0;
      this.monthlyExpenses.map((e) => {
        total = total + parseFloat(e.amount);
      });
      return total;
    },
    monthlyNet: function () {
      return (
        parseFloat(this.monthlyIncome) - parseFloat(this.totalMonthlyExpenses)
      );
    },
  },
  created() {
    const existingIncome = JSON.parse(localStorage.getItem("monthlyIncome"));
    const existingExpenses = JSON.parse(
      localStorage.getItem("monthlyExpenses")
    );

    if (existingIncome) {
      this.monthlyIncome = parseFloat(existingIncome);
    }
    if (existingExpenses) {
      this.monthlyExpenses = existingExpenses;
    }
  },
};
</script>
