<template>
  <div class="boards-page">
    <!-- list container -->
    <div class="lists--section">
      <List v-for="(listData, i) in lists" :key="i"/>
      <CreateList/>
    </div>
  </div>
</template>

<script>
import lists from '@/list-data';

export default {
  data() {
    return {
      lists,
    };
  },
  components: {
    List: () => import('@/components/boards-list/List'),
    CreateList: () => import('@/components/boards-list/CreateList'),
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
