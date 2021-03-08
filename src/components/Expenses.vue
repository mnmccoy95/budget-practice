<template>
  <div>
    <h3 class="teal--text">Add Expense</h3>
    <v-form @submit.prevent="handleSubmit" ref="expenses">
      <v-text-field
        outlined
        label="Name"
        v-model="expenses.name"
      ></v-text-field>
      <v-text-field
        outlined
        label="Amount"
        v-model="expenses.amount"
      ></v-text-field>
      <v-btn type="submit" color="teal" dark>Add</v-btn>
    </v-form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      expenses: {
        name: "",
        amount: "",
      },
    };
  },
  methods: {
    handleSubmit() {
      const isValid = this.$refs.expenses.validate();
      if (!isValid) {
        // Form is not valid. Exit the method
        return;
      }

      this.$emit("expenses-submit", this.expenses);
      this.expenses = {
        name: "",
        amount: "",
      };
      this.$refs.expenses.resetValidation();
    },
  },
};
</script>

<style>
</style>