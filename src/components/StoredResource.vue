<template>
  <ul>
    <item-resource
      v-for="storedResource in storedResources"
      :key="storedResource.id"
      :id="storedResource.id"
      :title="storedResource.title"
      :description="storedResource.description"
      :link="storedResource.link"
    ></item-resource>
  </ul>
</template>

<script>
import ItemResource from './ItemResource.vue';
export default {
  components: {
    ItemResource
  },
  inject: ['storedResources']
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
