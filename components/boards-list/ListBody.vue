<template>
  <div class="list--body">
    <div class="overflow-test"></div>
    <draggable class="list-group" :list="cards" group="people">
      <template v-for="(card, i) in cards">
        <div class="card" :key="i">
          {{card.text}}
        </div>
      </template>
    </draggable>
  </div>
</template>

<script>
import Draggable from 'vuedraggable';

export default {
  components: {
    Draggable,
  },
  props: {
    listData: {
      type: Object,
      required: false,
      default: () => ({}),
    },
  },
  data() {
    return {
      cards: this.listData.cards,
    };
  },
};
</script>

<style lang="scss">
.list--body {
  max-height: 100%;
  overflow-y: auto;

  .overflow-test{
    height: 1000px;
  }
}
</style>
