<template>
  <div class="list--body">
    <!-- <div class="overflow-test"></div> -->
    <draggable v-bind="dragOptions" class="cards-container" :list="listData.cards" group="people">
      <template v-for="(card, i) in listData.cards">
        <div class="card" :key="i">
          <!-- edit dialog -->
          <v-menu
            offset-y
            nudge-left="230px"
            nudge-top="20px"
            :close-on-content-click="cardUpdated"
          >
            <template v-slot:activator="{ on, attrs }">
              <button v-on="on" v-bind="attrs" class="edit-button"
                @click.prevent="editedCardText = card.text;
                cardUpdated=false"
              >
                <img class="edit-img" src="@/assets/edit-button.png" alt="edit">
              </button>
            </template>
            <v-card width="250px">
              <v-textarea v-model="editedCardText"/>
              <v-btn small color="green"
                dark @click="card.text = editedCardText; cardUpdated = true"> save</v-btn>
                <v-btn small color="orange"
                dark @click="deleteCard(i)"> Delete Card</v-btn>
            </v-card>
          </v-menu>
          <!-- edit dialog end -->
          <div class="card-content">
            <p class="card-text">{{card.text}}</p>
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
  data() {
    return {
      editedCardText: '',
      cardUpdated: false,
    };
  },
  computed: {
    dragOptions: () => ({
      animation: 60,
      group: 'description',
      disabled: false,
      ghostClass: 'ghost',
    }),
  },
  methods: {
    deleteCard(i) {
      const cardsData = this.listData.cards;
      cardsData.splice(i, 1);
    },
  },
};
</script>

<style lang="scss">
.list--body {
  min-height: 30px;
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
      position: relative;
      cursor: pointer;
      width:100%;
      height: fit-content;
      min-height: 32px;
      background-color: white;
      border-radius: 3px;
      margin-bottom: 8px;
      box-shadow: 0 1px 0 rgba(9,30,66,.25);
      padding: 6px 8px 2px;

      &:hover {
        background-color: #f4f5f6;

        .edit-button {
          display: flex;
        }
      }
      &:last-child {
        margin:0;
      }

      .edit-button{
        display: none;
        justify-content: center;
        align-items: center;
        width:20px;
        height: 20px;
        overflow: hidden;
        position: absolute;
        border-radius: 5px;
        top:0;
        right:0;
        outline: none;

        &:hover {
          background-color: rgba(0,0,0,.16);
        }

        .edit-img {
          width:70%;
          height: auto;
        }
      }

      .card-content {
        .card-text {
          width:100%;
          overflow: hidden;
          margin: 0;
        }
      }
    }
  }
}
</style>
