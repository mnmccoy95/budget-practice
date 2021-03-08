<template>
  <v-card>
    <v-card-title class="primary--text">Monthly Income</v-card-title>
    <v-card-text>
      <v-form @submit.prevent="saveIncome">
        <v-text-field
          @blur="saveIncome"
          v-model="monthlyAmount"
          type="number"
          outlined
          color="pink"
          filled
          prefix="$"
        />
      </v-form>
    </v-card-text>
  </v-card>
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