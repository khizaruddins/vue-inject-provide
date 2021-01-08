<template>
  <ul>
    <learning-resource
      v-for="res in resources"
      :title="res.title"
      :description="res.description"
      :key="res.id"
      :id="res.id"
      :link="res.link"
    ></learning-resource>
  </ul>
</template>

<script>
import LearningResource from "./LearningResource.vue";
export default {
  components: {
    LearningResource,
  },
  inject: ["resources"],
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
  margin: auto;
  max-width: 40rem;
}
</style>
