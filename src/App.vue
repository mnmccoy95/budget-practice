<template>
  <v-app>
    <v-main class="pa-6 pink lighten-4">
      <v-row justify="center">
        <v-col :cols="12" :md="8" :lg="4">
          <MonthlyIncome
            :monthlyAmount="monthlyIncome"
            @income-submit="updateIncome"
          />
        </v-col>
        <v-col :cols="12" :md="6" :lg="4">
          <IncomeCard :monthlyNet="this.monthlyNet" />
        </v-col>
      </v-row>
      <v-row>
        <v-col :cols="12" :lg="6">
          <Expenses
            :expenses="monthlyExpenses"
            @expenses-submit="addExpense"
            @expense-deleted="handleExpenseDeleted"
          />
        </v-col>
        <v-col :cols="12" :lg="6">
          <PieChart :expenses="monthlyExpenses" :totalAmount="annualExpenses" />
        </v-col>
      </v-row>
    </v-main>
  </v-app>
</template>

<script>
import MonthlyIncome from "./components/MonthlyIncome";
import Expenses from "./components/Expenses";
import IncomeCard from "./components/IncomeCard";
import PieChart from "./components/PieChart";

export default {
  components: {
    MonthlyIncome,
    Expenses,
    IncomeCard,
    PieChart,
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
    handleExpenseDeleted(expense) {
      this.monthlyExpenses = this.monthlyExpenses.filter((e) => {
        return e !== expense;
      });
      localStorage.setItem(
        "monthlyExpenses",
        JSON.stringify(this.monthlyExpenses)
      );
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
    annualExpenses() {
      return this.totalMonthlyExpenses * 12;
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
