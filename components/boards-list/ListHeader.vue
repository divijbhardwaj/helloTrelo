<template>
  <div class="list--header drag-handle">
    <input class="list-title"
      @focus="editable = true" @blur="()=>editable = false"
      :class="editable? 'editable': 'not-editable'" type="text" v-model="value"/>
    <ListOptions @del-list="deleteList(listData.title)"/>
  </div>
</template>

<script>
export default {
  inject: ['deleteList'],
  components: {
    ListOptions: () => import('@/components/boards-list/ListOptions'),
  },
  props: {
    listData: {
      type: Object,
      required: false,
      default: () => ({}),
    },
  },
  watch: {
    value: {
      handler() {
        const ld = this.listData;
        ld.title = this.value;
      },
      deep: true,
    },
    listData: {
      handler() {
        this.value = this.listData.title;
      },
      deep: true,
      immediate: true,
    },
  },
  data() {
    return {
      value: '',
      editable: false,
    };
  },
};
</script>

<style lang="scss">
.list--header {
  cursor: pointer;
  width:100%;
  height:40px;
  padding: 10px;
  display: flex;
  flex-wrap: nowrap;
  align-items: center;

  .list-title {
    flex:1;
    cursor: pointer;
    height:100%;
    width:100%;
    margin-right:8px;
    border-radius: 3px;
    outline: none;
    text-indent: 5px;

    &.editable {
      background-color: white;
      outline: 1px solid rgb(0, 183, 255);
    }
    &.not-editable {
      background-color: transparent;
    }
  }
}
</style>
