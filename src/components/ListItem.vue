<template>
  <div class="list-item" v-for="item in items" :key="item">
    <div class="wrapper_item">
      <input type="checkbox" v-model="item.selected" @change="updateItem" />
      <span>Item {{ item.id }}</span>
    </div>
    <div class="wrapper_cube">
      <input type="number" min="0" v-model="item.quantity" class="input-number" />
      <input class="color-cube" type="color" v-model="item.color" @input="updateColor" />
    </div>
  </div>
</template>

<script>
export default {
  name: "ListItem",
  emits: ["update-item"],
  data() {
    return {};
  },
  props: {
    items: {
      type: Array,
      required: true,
    },
  },
  methods: {
    updateColor() {
      this.updateItem();
    },
    updateItem() {
      this.$emit("update-item");
    },
  },
};
</script>

<style scoped>
.list-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 5px 0;
}
.color-cube {
  width: 20px;
  height: 20px;
  margin-left: 10px;
  padding: 0;
  border: none;
}
.wrapper_cube {
  display: flex;
  align-items: center;
}
.input-number {
  width: 30px;
  border: none;
}
</style>
