<template>
  <div id="app">
    <div class="wrapper_lists">
      <lists-panel :lists="lists"></lists-panel>
    </div>
    <div class="wrapper_view-panel">
      <view-panel :lists="lists"></view-panel>
    </div>
  </div>
</template>

<script>
import ListsPanel from "./components/ListsPanel.vue";
import ViewPanel from "./components/ViewPanel.vue";
import { reactive } from "vue";

export default {
  name: "App",
  components: {
    ListsPanel,
    ViewPanel,
  },
  data() {
    return {
      lists: reactive([
        {
          id: 1,
          name: "List 1",
          showItems: false,
          items: [
            { id: 1, selected: false, quantity: 1, color: "#FF0000" },
            { id: 2, selected: false, quantity: 2, color: "#32CD32" },
            { id: 3, selected: false, quantity: 3, color: "#0000CD" },
            { id: 4, selected: false, quantity: 1, color: "#FFD700" },
          ],
        },
        {
          id: 2,
          name: "List 2",
          showItems: false,
          items: [
            { id: 1, selected: false, quantity: 1, color: "#FF0000" },
            { id: 2, selected: false, quantity: 2, color: "#32CD32" },
            { id: 3, selected: false, quantity: 3, color: "#0000CD" },
            { id: 4, selected: false, quantity: 1, color: "#FFD700" },
            { id: 5, selected: false, quantity: 1, color: "#FF7F50" },
          ],
        },
        {
          id: 3,
          name: "List 3",
          showItems: false,
          items: [
            { id: 1, selected: false, quantity: 1, color: "#FF0000" },
            { id: 2, selected: false, quantity: 2, color: "#32CD32" },
            { id: 3, selected: false, quantity: 3, color: "#0000CD" },
            { id: 4, selected: false, quantity: 1, color: "#FFD700" },
            { id: 5, selected: false, quantity: 1, color: "#FF7F50" },
          ],
        },
        {
          id: 4,
          name: "List 4",
          showItems: false,
          items: [
            { id: 1, selected: false, quantity: 1, color: "#FF0000" },
            { id: 2, selected: false, quantity: 2, color: "#32CD32" },
            { id: 3, selected: false, quantity: 3, color: "#0000CD" },
            { id: 4, selected: false, quantity: 1, color: "#FFD700" },
            { id: 5, selected: false, quantity: 1, color: "#FF7F50" },
          ],
        },
        {
          id: 5,
          name: "List 5",
          showItems: false,
          items: [
            { id: 1, selected: false, quantity: 1, color: "#FF0000" },
            { id: 2, selected: false, quantity: 2, color: "#32CD32" },
            { id: 3, selected: false, quantity: 3, color: "#0000CD" },
            { id: 4, selected: false, quantity: 1, color: "#FFD700" },
            { id: 5, selected: false, quantity: 1, color: "#FF7F50" },
          ],
        },
      ]),
    };
  },
};
</script>

<style>
#app {
  width: 100vw;
  display: flex;
}
.wrapper_lists {
  width: 40%;
  display: flex;
  flex-direction: column;
  margin-left: 10%;
}
.wrapper_view-panel {
  width: 40%;
  display: flex;
  flex-direction: column;
  margin: 0 0 0 20px;
}
</style>
