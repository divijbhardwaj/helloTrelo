<template>
  <div class="boards-page">
    <section class="lists--section--wrapper">
      <!-- lists -->
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
              <!-- <CreateList @create-list="createList"/> -->
      </draggable>
      <!-- create lists -->
      <CreateList @create-list="createList"/>
    </section>
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

  .lists--section--wrapper {
    height: 100%;
    width:100%;
    display: flex;
    justify-content: flex-start;
    overflow-x: auto;

    .lists--section {
      height:100%;
      width:fit-content;
      display: flex;
      flex-flow: row nowrap;
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
}

</style>
