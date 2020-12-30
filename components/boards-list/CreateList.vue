<template>
  <button class="create-list--button" @click="createList">
    <span>Add another list</span>
  </button>
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

<style lang="scss">
  .create-list--button {
    width: 272px;
    height:40px;
    border-radius: 3px;
    background-color: rgba(0,0,0,.08);
    outline: none;
    padding:0 12px;
    text-align: left;

    span{
      white-space: nowrap;
      line-height: 1;
      color: #172b4d;
      &::before {
        margin-right: 10px;
        font-size: 22px;
        content: '+'
      }
    }

    &:hover {
      background-color: rgba(0,0,0,.16);
    }
  }
</style>
