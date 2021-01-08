<template>
  <li>
    <base-card>
      <header>
        <h3>{{ title }}</h3>
        <base-button mode="flat" @click="handleDelete()">Delete</base-button>
      </header>
      <p>{{ description }}</p>
      <nav>
        <a :href="link">View Resource</a>
      </nav>
    </base-card>
  </li>
</template>

<script>
export default {
  inject: ["deleteResource"],
  props: ["id", "title", "description", "link"],
  methods: {
    handleDelete() {
      this.deleteResource(this.id);
    },
  },
};
</script>

<style lang="css" scoped></style>
