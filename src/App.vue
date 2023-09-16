<script lang="ts">
import TheHeader from './components/TheHeader.vue';
import TheTodoList from './components/TheTodoList.vue';
import { defineComponent } from 'vue';
import { Item } from './types/types';

interface State {
  basketItems: Item[];
}

export default defineComponent({
  components: {
    TheHeader,
    TheTodoList,
  },
  data(): State {
    return {
      basketItems: [],
    };
  },
  created() {
    const storedItems = localStorage.getItem('basketItems');
    if (storedItems) {
      this.basketItems = JSON.parse(storedItems);
    }
  },
  methods: {
    addItem(item: Item) {
      this.basketItems.push(item);
      this.saveToLocalStorage();
    },
    toggleItem(id: string) {
      const index = this.basketItems.findIndex(item => item.id === id);
      if (index !== -1) {
        this.basketItems[index].completed = !this.basketItems[index].completed;
        this.saveToLocalStorage();
      }
    },
    removeItem(id: string) {
      this.basketItems = this.basketItems.filter(
        (elem: Item) => elem.id !== id,
      );
      this.saveToLocalStorage();
    },
    saveToLocalStorage() {
      localStorage.setItem('basketItems', JSON.stringify(this.basketItems));
    },
  },
  computed: {
    sortedBasketItems(): Item[] {
      const copiedArr = [...this.basketItems];
      console.log(copiedArr);
      return copiedArr.sort((a, b) =>
        a.completed === b.completed ? 0 : a.completed ? 1 : -1,
      );
    },
  },
});
</script>

<template>
  <TheHeader @add-item="addItem" />
  <main class="main">
    <TheTodoList
      :basketItems="sortedBasketItems"
      @toggle-item="toggleItem"
      @remove-item="removeItem" />
  </main>
</template>

<style lang="scss">
.main {
  margin: 0 auto;
  max-width: 480px;
  min-height: 50vh;
  text-align: center;
  overflow: hidden;
  padding: 1rem;
  border-radius: 10px;
  box-shadow: 2px 3px 10px rgba(0, 0, 0, 0.2);
  background: #fff;
  margin-top: 7rem;
  padding-left: 2%;
  padding-right: 2%;

  @media screen and (max-width: 480px) {
    max-width: 280px;
  }
}
</style>
