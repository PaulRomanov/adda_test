<template>
<div class="view-panel">
    <div class="list-view" v-for="list in filteredLists" :key="list.id">
      <h3>{{ list.name }}</h3>
      <div class="selected-items">
        <div v-for="item in list.items" :key="item.id" class="selected-item">
          <div
            v-for="cube in item.quantity"
            :key="cube"
            class="color-cube"
            :style="{ backgroundColor: item.color }"
          ></div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ViewPanel",
  data() {
    return {};
  },
  props: { lists: Array,},
  computed: {
    filteredLists() {
      return this.lists.map((list) => ({
        ...list,
        items: list.items.filter((item) => item.selected),
      }));
    },
  },
};
</script>

<style scoped>
.view-panel {
  display: flex;
  flex-direction: column;
}

.list-view {
  margin: 10px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  background-color: #f9f9f9;
}

.selected-items {
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;
  margin-top: 10px;
}

.selected-item {
  display: flex;
  align-items: center;
  margin-right: 10px;
  margin-bottom: 5px;
}

.color-cube {
  width: 20px;
  height: 20px;
  margin-right: 5px;
  border: 1px solid #000;
}
</style>