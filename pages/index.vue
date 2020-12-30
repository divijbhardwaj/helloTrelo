<template>
  <div class="boards-page">
    <!-- {{lists}} -->
    <!-- list container -->
    <!-- <div class="lists--section"> -->

       <draggable
        class="lists--section"
        tag="div"
        v-model="lists"
        v-bind="dragOptions"
        handle=".drag-handle"
        @start="isDragging = true"
        @end="isDragging = false"
      >
        <template v-for="(listData, i) in lists">
          <List
            :list-data="listData"
            aria-hidden="true" :key="i"/>
        </template>
       </draggable>
       <CreateList @create-list="createList"/>
    <!-- </div> -->
  </div>
</template>

<script>
import lists from '@/list';
import Draggable from 'vuedraggable';

export default {
  data() {
    return {
      lists,
      isDragging: false,
    };
  },
  components: {
    List: () => import('@/components/boards-list/List'),
    CreateList: () => import('@/components/boards-list/CreateList'),
    Draggable,
  },
  computed: {
    dragOptions: () => ({
      animation: 200,
      group: 'description',
      disabled: false,
      ghostClass: 'ghost',
    }),
  },

  methods: {
    createList(listData) {
      this.lists.push({ title: 'dsf ', cards: [] });
    },
  },

};
</script>

<style lang="scss">
.boards-page{
  height: 100%;
  max-height: 100vh;
  padding:8px;

  .lists--section {
    height:100%;
    width:100%;
    display: flex;
    flex-flow: row nowrap;
    overflow-x: auto;
    padding-bottom:8px;

    .ghost {
      position: relative;
      background-color: transparent;

      >div {
        opacity: 0;
      }
      &::after {
        content:' ';
        position: absolute;
        border-radius: 3px;
        top:0;
        left: 0;
        width:100%;
        height:100%;
        background-color: rgba(0,0,0,.32);
      }
    }
  }
}

</style>
