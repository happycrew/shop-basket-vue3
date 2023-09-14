<script lang="ts">
import TheHeader from './components/TheHeader.vue';
import TheTodoList from './components/TheTodoList.vue';
import { defineComponent } from 'vue';

export default defineComponent({
  components: {
    TheHeader,
    TheTodoList,
  },
  data: () => ({
    basketItems: [
      { id: 0, text: 'Apples', completed: true },
      { id: 1, text: 'Banana', completed: true },
      { id: 2, text: 'Juice', completed: false },
    ],
    someTitle: 'random string',
  }),
});
</script>

<template>
  <TheHeader />
  <main class="main pt-5">
    <TheTodoList :basketItems="basketItems" />
  </main>
</template>

<style lang="scss">
.main {
  margin: 0 auto;
  min-width: 300px;
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
}
</style>
