<template>
  <div>
    <h3>Monthly Leftover</h3>
    <span>{{ monthlyNet }}</span>
  </div>
</template>

<script>
export default {
  props: ["monthlyNet"],
};
</script>

<style>
</style>