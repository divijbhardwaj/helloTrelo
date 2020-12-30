<template>
  <div class="list--footer" @click="createCard">
    create card
  </div>
</template>

<script>
export default {
  methods: {
    createCard() {
      this.$emit('create-card');
    },
  },
};
</script>

<style lang="scss">
.list--footer{
  width:100%;
  height:38px;
}
</style>
