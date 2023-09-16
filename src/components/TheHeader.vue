<script lang="ts">
import { defineComponent } from 'vue';
import TheForm from './TheForm.vue';
import { Item } from '@/types/types';
export default defineComponent({
  components: {
    TheForm,
  },
  methods: {
    addItem(item: Item) {
      this.$emit('addItem', item);
    },
  },
  emits: {
    addItem: (item: Item) => item,
  },
});
</script>

<template>
  <header class="header">
    <h2 class="logo">Shop Basket</h2>
    <TheForm @add-item="addItem" />
  </header>
</template>

<style scoped lang="scss">
@import '../assets/styles/variables.scss';
.header {
  position: sticky;
  top: 0;
  z-index: 20;
  display: flex;
  align-items: center;
  justify-content: space-between;
  border-bottom-width: 1px;
  background: #eeeeee;
  box-shadow: $box-shadow;
  padding: 0.95rem;
  @media screen and (max-width: 720px) {
    flex-direction: column;
    gap: 10px;
  }
}

.logo {
  margin-left: 1.95rem;
  @media screen and (max-width: 720px) {
    margin-left: 0;
  }
}
</style>
