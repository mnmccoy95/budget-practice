<template>
  <v-card>
    <v-card-title class="primary--text"> Monthly Expenses </v-card-title>
    <v-card-text>
      <v-simple-table :height="200">
        <template v-slot:default>
          <thead>
            <tr>
              <th class="secondary--text">Name</th>
              <th class="secondary--text">Amount</th>
              <th></th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="expense in expenses" :key="expense.name">
              <td>{{ expense.name }}</td>
              <td>${{ expense.amount }}</td>
              <td class="text-right">
                <v-btn
                  fab
                  x-small
                  color="red"
                  dark
                  @click="handleDelete(expense)"
                >
                  <v-icon>mdi-minus</v-icon>
                </v-btn>
              </td>
            </tr>
          </tbody>
        </template>
      </v-simple-table>
      <v-divider></v-divider>
      <h4 class="my-3 secondary--text">Add Expense</h4>
      <v-form @submit.prevent="handleSubmit">
        <v-row>
          <v-col :sm="5">
            <v-text-field
              v-model="name"
              color="pink"
              outlined
              filled
              dense
              placeholder="Name"
            />
          </v-col>
          <v-col :sm="5">
            <v-text-field
              v-model="amount"
              type="number"
              color="pink"
              outlined
              filled
              dense
              placeholder="Cost"
              prefix="$"
            />
          </v-col>
          <v-col :sm="2">
            <v-btn fab small color="pink lighten-3" dark type="submit">
              <v-icon>mdi-plus</v-icon>
            </v-btn>
          </v-col>
        </v-row>
      </v-form>
    </v-card-text>
  </v-card>
</template>

<script>
export default {
  props: ["expenses"],
  data() {
    return {
      name: "",
      amount: null,
    };
  },
  methods: {
    handleSubmit() {
      this.$emit("expenses-submit", { name: this.name, amount: +this.amount });
      this.expenses = {
        name: "",
        amount: null,
      };
    },
    handleDelete(expense) {
      this.$emit("expense-deleted", expense);
    },
  },
};
</script>

<style>
/* width */
::-webkit-scrollbar {
  width: 10px;
}

/* Track */
::-webkit-scrollbar-track {
  background: #f1f1f1;
}

/* Handle */
::-webkit-scrollbar-thumb {
  background: #e7a1b9;
}

/* Handle on hover */
::-webkit-scrollbar-thumb:hover {
  background: #ec407a;
}
</style>