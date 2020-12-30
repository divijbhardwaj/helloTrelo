<template>
  <div class="list--header drag-handle" @click="handleHeaderClick">
    <input @click="handleFieldClick" type="text" :value="listData.title"/>
  </div>
</template>

<script>
export default {
  props: {
    listData: {
      type: Object,
      required: false,
      default: () => ({}),
    },
  },
  data() {
    return {
      value: 'sdf',
    };
  },
  methods: {
    handleFieldClick() {
      console.log('field-clicked');
    },
    handleHeaderClick() {
      console.log('header-clicked');
    },
  },
};
</script>

<style lang="scss">
.list--header {
  width:100%;
  height:40px;
  padding: 10px;

  input {
    height:100%;
    width:100%;
    background-color: white;
  }
}
</style>
