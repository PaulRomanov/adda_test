<template>
  <div class="view-panel">
    <div class="list-view" v-for="list in filteredLists" :key="list.id">
      <div class="wrapper">
        <h3>{{ list.name }}</h3>
        <button @click="btnAction(list)">{{ buttonText(list) }}</button>
      </div>
      <div class="selected-items">
        <div v-if="list.showShuffleButton">
          <div v-for="item in list.items" :key="item.id" class="selected-item">
            <div
              v-for="cube in item.quantity"
              :key="cube"
              class="color-cube"
              :style="{ backgroundColor: item.color }"
              @click="removeCube(list, item)"
            ></div>
          </div>
        </div>
        <div class="selected-item" v-else>
          <div
            v-for="sortCube in list.shuffledCubes"
            :key="sortCube.color"
            class="color-cube"
            :style="{ backgroundColor: sortCube.color }"
          ></div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import cloneDeep from "lodash/cloneDeep";

export default {
  name: "ViewPanel",
  data() {
    return {};
  },
  props: { lists: Array },
  computed: {
    filteredLists() {
      return this.lists.map((list) => {
        const selectedItems = list.items.filter((item) => item.selected);
        return {
          ...list,
          items: selectedItems,
          showShuffleButton: true,
          shuffledCubes: [],
          originalItems: this.copyOriginalItems(selectedItems), // копия оригинальных элементов. Копируем только выбранные элементы
        };
      });
    },
  },
  methods: {
    copyOriginalItems(selectedItems) {
      return cloneDeep(selectedItems);
    },
    btnAction(list) {
      if (list.showShuffleButton) {
        list.shuffledCubes = this.shuffleCubes(list.items);
      } else {
        this.restoreOriginalItems(list);
      }
      list.showShuffleButton = !list.showShuffleButton;
    },
    buttonText(list) {
      return list.showShuffleButton ? "Перемешать" : "Сортировать";
    },

    shuffleCubes(array) {
      let newArray = [];
      //создаем массив объектов, только для элементов с количеством больше нуля
      // где каждый объект - это кубик определенного цвета
      for (let i = 0; i < array.length; i++) {
        if (array[i].quantity > 0) {
          newArray = newArray.concat(
            Array(array[i].quantity).fill({
              color: array[i].color,
            })
          );
        }
      }
      // Перемешиваем массив объектов
      for (let i = newArray.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [newArray[i], newArray[j]] = [newArray[j], newArray[i]];
      }
      this.$forceUpdate();
      return newArray;
    },

    restoreOriginalItems(list) {
      const originalList = this.lists.find((l) => l.id === list.id);
      if (originalList) {
        // Заменяем только элементы с количеством больше нуля
        for (let i = 0; i < originalList.items.length; i++) {
          if (originalList.items[i].quantity === 0) {
            originalList.items.splice(i, 1);
            i--;
          }
        }
      }
      this.$forceUpdate();
    },
    saveOriginalItems(list) {
      this.originalItems[list.id] = list.items.map((item) => ({ ...item }));
    },
    removeCube(list, item) {
      if (item.quantity > 0) {
        item.quantity--;
        if (item.quantity === 0) {
          const itemIndex = list.items.indexOf(item);
          if (itemIndex > -1) {
            list.items.splice(itemIndex, 1);
          }
          item.selected = false;
        }
      }
    },
  },
};
</script>

<style scoped>
.view-panel {
  display: flex;
  flex-direction: column;
}

.wrapper {
  display: flex;
  justify-content: space-between;
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
  flex-wrap: wrap;
  margin-right: 10px;
  margin-bottom: 5px;
}

.color-cube {
  width: 20px;
  height: 20px;
  margin-right: 5px;
  margin-top: 5px;
  border: 1px solid #000;
}
button {
  border-radius: 5px;
  background-color: #599feb;
  color: white;
  height: 40px;
  cursor: pointer;
}
</style>
