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
        @start="drag = true"
        @end="drag = false"
      >
        <template v-for="(listData, i) in lists">
          <List  @click="listData.fixed = !listData.fixed" aria-hidden="true" :key="i"/>
        </template>
              <CreateList @create-list="createList"/>
       </draggable>
    <!-- </div> -->
  </div>
</template>

<script>
import lists from '@/list-data';
import draggable from 'vuedraggable';

export default {
  data() {
    return {
      lists,
      drag: false,
    };
  },
  components: {
    List: () => import('@/components/boards-list/List'),
    CreateList: () => import('@/components/boards-list/CreateList'),
    draggable,
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
      lists.push({ header: 'new-list' });
    },
  },

};
</script>

<style lang="scss" scoped>
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
  }
}
</style>
