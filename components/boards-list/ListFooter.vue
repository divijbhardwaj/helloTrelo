<template>
  <div class="list--footer">
    <!-- edit card dialog -->
    <v-menu
      offset-y
      nudge-top="28px"
      :close-on-content-click="cardUpdated"
    >
      <template v-slot:activator="{ on, attrs }">
        <button v-on="on" v-bind="attrs" class="create-card--button"
        @click.prevent="text='';cardUpdated=false">
          <span>Add another card</span>
        </button>
      </template>
      <v-card width="250px">
        <v-textarea v-model="text"/>
        <v-btn small color="green"
          dark @click="createCard();cardUpdated = true;">Add card</v-btn>
      </v-card>
    </v-menu>
    <!-- edit card dialog ends -->
  </div>
</template>

<script>
export default {
  data() {
    return {
      cardUpdated: false,
      text: '',
    };
  },
  methods: {
    createCard() {
      this.$emit('create-card', this.text);
    },
  },
};
</script>

<style lang="scss">
.list--footer{
  width:100%;
  // height:38px;
  padding: 0 8px 8px;

  .create-card--button {
    width: 100%;
    height:28px;
    border-radius: 3px;
    outline: none;
    padding:0 12px;
    text-align: left;

    span{
      white-space: nowrap;
      line-height: 1;
      color: #172b4d;
      &::before {
        margin-right: 10px;
        font-size: 22px;
        content: '+'
      }
    }

    &:hover {
      background-color: rgba(0,0,0,.08);
    }
  }
}
</style>
