<template>
  <div class="list--container">
    <ListHeader :listData="listData"/>
    <ListBody :listData="listData"/>
    <ListFooter @create-card="createCard" :listData="listData"/>
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
      lData: this.listData,
    };
  },
  components: {
    ListHeader: () => import('@/components/boards-list/ListHeader'),
    ListBody: () => import('@/components/boards-list/ListBody'),
    ListFooter: () => import('@/components/boards-list/ListFooter'),
  },
  methods: {
    createCard() {
      this.lData.cards.push({ text: 'bye' });
    },
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
  }
</style>
