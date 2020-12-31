<template>
  <div class="boards-page">
    <!-- {{lists}} -->
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
      </draggable>
      <!-- create lists -->
      <CreateList :lists="lists" @create-list="createList"/>
    </section>
  </div>
</template>

<script>
import lists from '@/list';
import Draggable from 'vuedraggable';
import List from '@/components/boards-list/List';

export default {
  provide() {
    return {
      deleteList: this.deleteList,
    };
  },
  data() {
    return {
      lists,
      isDragging: false,
    };
  },
  components: {
    List,
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
    createList(title) {
      this.lists.push({ title, cards: [] });
    },
    deleteList(delTitle) {
      const con = confirm(`You are about to delete the "${delTitle}" list`);
      if (!con) {
        return;
      }
      this.lists = this.lists.filter(({ title }) => title !== delTitle);
    },
  },

};
</script>

<style lang="scss">
.boards-page{
  background-image: url("https://trello-backgrounds.s3.amazonaws.com/5e627d9fa6c99f7637f32c47/2560x1440/e93a3b56f1e677578e6059be2d9f8694/crmble_trello_order-mgmt.png");
  background-position: 50%;
  background-size: cover;
  height: 100%;
  max-height: 100vh;
  padding:20px 20px 8px;

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
