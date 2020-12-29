<template>
  <div @click="createList">create list</div>
</template>

<script>
export default {
  methods: {
    createList() {
      this.$emit('create-list');
    },
  },
};
</script>

<style>

</style>
