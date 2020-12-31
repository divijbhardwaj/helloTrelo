<template>
  <v-menu
    offset-y
    nudge-top="28px"
    :close-on-content-click="listUpdated"
  >
    <template v-slot:activator="{ on, attrs }">
      <button v-on="on" v-bind="attrs"
        class="create-list--button" @click.prevent="title='';error='';listUpdated=false">
        <span>Add another list</span>
      </button>
    </template>
    <v-card width="250px">
      <v-text-field :error-messages="error" label="List Title" v-model="title"/>
      <v-btn small color="green"
        dark @click="validate">Add List</v-btn>
    </v-card>
  </v-menu>
</template>

<script>
export default {
  props: {
    lists: {
      type: Array,
      required: false,
      default: () => [],
    },
  },
  data() {
    return {
      listUpdated: false,
      title: '',
      error: '',
    };
  },
  methods: {
    validate() {
      const listExists = Boolean(this.lists.find((list) => list && list.title === this.title));
      if (listExists) {
        this.error = 'List already exists';
        return;
      }
      this.listUpdated = true;
      this.createList();
    },
    createList() {
      this.$emit('create-list', this.title);
    },
  },
};
</script>

<style lang="scss">
  .create-list--button {
    width: 272px;
    height:40px;
    border-radius: 3px;
    background-color: rgba(0,0,0,.08);
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
      background-color: rgba(0,0,0,.16);
    }
  }
</style>
