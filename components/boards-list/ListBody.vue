<template>
  <div class="list--body">
    <!-- <div class="overflow-test"></div> -->
    <draggable v-bind="dragOptions" class="cards-container" :list="listData.cards" group="people">
      <template v-for="(card, i) in listData.cards">
        <div class="card" :key="i">
          <div class="card-content">
            {{card.text}}
          </div>
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
  computed: {
    dragOptions: () => ({
      animation: 60,
      group: 'description',
      disabled: false,
      ghostClass: 'ghost',
    }),
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
  .cards-container {
    width:100%;
    display: flex;
    flex-direction: column;
    padding: 0 10px 10px;
    .card{
      cursor: pointer;
      width:100%;
      height: 32px;
      background-color: white;
      border-radius: 3px;
      margin-bottom: 8px;
      box-shadow: 0 1px 0 rgba(9,30,66,.25);
      padding: 6px 8px 2px;

      &:hover {
        background-color: #f4f5f6;
      }
      &:last-child {
        margin:0;
      }
    }
  }
}
</style>
