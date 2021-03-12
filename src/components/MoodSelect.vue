<template>
  <v-card>
    <v-card-title class="primary--text"> Mood Tracker </v-card-title>
    <v-card-text>
      <span v-for="mood in moods" :key="mood.name">
        <v-btn
          class="mx-1"
          fab
          dark
          small
          color="primary"
          @click="handleAdd(mood)"
          ><v-icon dark>{{ mood.icon }}</v-icon></v-btn
        >
      </span>
    </v-card-text>
    <MoodChart :moodCounts="moodCounts" />
  </v-card>
</template>

<script>
import { moodItems } from "./moods";
import MoodChart from "./MoodChart";

export default {
  props: ["moodCounts"],
  components: { MoodChart },
  data() {
    return {
      moods: [...moodItems],
    };
  },
  methods: {
    handleAdd(mood) {
      this.$emit("add-mood", mood);
    },
  },
};
</script>

<style>
</style>