<template>
  <div class="list" v-for="list in lists" :key="list.id">
    <div class="wrapper_list">
      <CheckBox @change="selectAllItems(list)"/>
      <h3 @click="toggleShowItems(list)">{{ list.name }}</h3>
    </div>
    <div class="wrapper_items" v-show="list.showItems">
      <ListItem :items="list.items"></ListItem>
    </div>
  </div>
</template>

<script>
import ListItem from "./ListItem.vue";
import CheckBox from "./CheckBox.vue";
export default {
  name: "ListPanel",
  components: {
    ListItem,
    CheckBox,
  },
  data() {
    return {

    };
  },
  props: {
    lists: {
      type: Array,
      required: true,
    },
  },
  methods: {
    toggleShowItems(list) {
      list.showItems = !list.showItems;
    },
    selectAllItems(list) {

      const allSelected = list.items.every((item) => item.selected);
      list.items = list.items.map((item) => ({ ...item, selected: !allSelected }));

    },
  },
};
</script>

<style scoped>
.list {
  margin: 5px 0;
  cursor: pointer;
}

.wrapper_list {
  display: flex;
  align-items: center;
}

.wrapper_items {
  display: flex;
  flex-direction: column;
  margin: 0 0 0 20px;
}
</style>
