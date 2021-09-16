<template>
  <base-card>
    <base-button @click="setSelectedTab('stored-resource')">Mémo</base-button>
    <base-button @click="setSelectedTab('add-resource')"
      >Ajouter Mémo</base-button
    >
  </base-card>
  <keep-alive>
    <component :is="selectedTab"></component>
  </keep-alive>
</template>

<script>
import StoredResource from './StoredResource.vue';
import AddResource from './AddResource.vue';

export default {
  components: {
    StoredResource,
    AddResource
  },
  data() {
    return {
      selectedTab: 'stored-resource',

      resources: [
        {
          id: 'facebook',
          title: 'Facebook',
          description: 'Réseaux sociaux',
          link: 'https://facebook.com'
        },
        {
          id: 'google',
          title: 'Google',
          description: 'Apprendre google',
          link: 'https://google.com'
        }
      ]
    };
  },
  provide() {
    return {
      storedResources: this.resources,
      addResource: this.addResource,
      deleteResource: this.deleteResource
    };
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    },
    addResource(title, description, url) {
      const newResource = {
        id: new Date().toISOString(),
        title: title,
        description: description,
        link: url
      };
      this.resources.unshift(newResource);
      this.selectedTab = 'stored-resource';
    },
    deleteResource(resId) {
      const resIndex = this.resources.findIndex(res => res.id === resId);
      this.resources.splice(resIndex, 1);
    }
  }
};
</script>

<style></style>
