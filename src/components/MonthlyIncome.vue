<template>
  <div>
    <h3 class="teal--text">Add Income</h3>
    <v-form>
      <v-text-field
        outlined
        label="Monthly Income"
        v-model="monthlyAmount"
        v-on:blur="saveIncome"
      ></v-text-field>
    </v-form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      monthlyAmount: "",
    };
  },
  methods: {
    saveIncome() {
      this.$emit("income-submit", this.monthlyAmount);
      localStorage.setItem("monthlyIncome", JSON.stringify(this.monthlyAmount));
    },
  },
};
</script>

<style>
</style>