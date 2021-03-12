<template>
  <v-card height="100%">
    <apexchart type="pie" :options="options" :series="series" height="300" />
  </v-card>
</template>

<script>
export default {
  props: ["moodCounts"],
  computed: {
    series() {
      return this.moodCounts.map((e) => e.count);
    },
    options() {
      return {
        labels: this.moodCounts.map((e) => e.name),

        colors: [
          "#ff6663",
          "#feb144",
          "#fdfd97",
          "#9ee09e",
          "#9ec1cf",
          "#CC99C9",
        ],
      };
    },
  },
};
</script>

<style></style>