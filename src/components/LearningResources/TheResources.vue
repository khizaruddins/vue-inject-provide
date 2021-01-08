<template>
  <div>
    <base-card>
      <base-button :mode="storedResButtonMode" @click="setSelectedTab('stored-resources')"
        >Stored Resource
      </base-button>
      <base-button :mode="addResButtonMode" @click="setSelectedTab('add-resource')"
        >Add Resource
      </base-button>
    </base-card>
    <component :is="selectedTab"></component>
  </div>
</template>
<script>
import StoredResources from "./StoredResources.vue";
import AddResource from "./AddResource.vue";
export default {
  provide() {
    return {
      resources: this.storedResources,
      addResource: this.addResource,
      deleteResource: this.deleteResource,
    };
  },
  computed: {
    storedResButtonMode() {
      return this.selectedTab === "stored-resources" ? null : "flat";
    },
    addResButtonMode() {
      return this.selectedTab === "add-resource" ? null : "flat";
    },
  },
  components: {
    StoredResources,
    AddResource,
  },
  data() {
    return {
      selectedTab: "stored-resources",
      storedResources: [
        {
          id: "official-guide",
          title: "Official Guide",
          description: "The Official Vue.js documentation",
          link: "https://vuejs.org",
        },
        {
          id: "google",
          title: "Google",
          description: "Learn to Google",
          link: "https://www.google.com",
        },
      ],
    };
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    },
    addResource(formData) {
      this.storedResources.unshift({
        id: new Date().toISOString(),
        title: formData.title,
        description: formData.description,
        link: formData.link,
      });
      this.selectedTab = "stored-resources";
    },
    deleteResource(id) {
      const index = this.storedResources.findIndex((item) => item.id === id);
      this.storedResources.splice(index, 1);
    },
  },
};
</script>
