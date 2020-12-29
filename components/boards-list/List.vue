<template>

  <div class="list--container">
    <ListHeader />
    <ListBody />
    <ListFooter />
  </div>

</template>

<script>
export default {
  components: {
    ListHeader: () => import('@/components/boards-list/ListHeader'),
    ListBody: () => import('@/components/boards-list/ListBody'),
    ListFooter: () => import('@/components/boards-list/ListFooter'),
  },
};
</script>

<style lang="scss">
  .list--container {
    border-radius: 3px;
    background-color: var(--list-bg);
    display: flex;
    flex-direction: column;
    height: fit-content;
    max-height: 100%;
    min-width: var(--max-list-width);
    max-width: var(--max-list-width);
    margin-right:8px;

    &:last-child {
      margin-right: 0;
    }
  }
</style>
