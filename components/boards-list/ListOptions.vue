<template>
  <v-menu offset-y>
    <template v-slot:activator="{ on }">
      <button class="list-options-button" v-on="on">...</button>
    </template>
    <v-list>
      <v-list-item
        v-for="(item, index) in items"
        :key="index"
      >
        <v-list-item-title @click="item.action">{{ item.title }}</v-list-item-title>
      </v-list-item>
    </v-list>
  </v-menu>
</template>

<script>
export default {
  computed: {
    items() {
      return [
        { title: 'Delete List', action: () => this.$emit('del-list') },
      ];
    },
  },
};
</script>

<style lang="scss">
  .list-options-button {
    width:32px;
    height:32px;
    line-height: 0;
    border-radius:3px;

    &:hover{
      background-color: rgba(0,0,0,.16);
    }
  }
</style>
