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
}

.logo {
  margin-left: 1.95rem;
}

.form {
  display: flex;
  margin-right: 120px;

  &__input {
    width: 380px;
    background: #fff;
    color: $input-text-color;
    font: inherit;
    box-shadow: 0 6px 10px 0 rgba(0, 0, 0, 0.1);
    border: 0;
    outline: 0;
    padding: 0.75rem;
  }

  &__btn {
    align-self: center;
    text-align: center;
    background: transparent;
    color: inherit;
    width: 60px;
    height: 35px;
    border: 0;
    transition: all 200ms ease-in-out;
    cursor: pointer;
    text-transform: uppercase;
    margin-left: -35px;

    &--primary {
      background: $button-bg-color;
      color: $button-text-color;
      box-shadow: 0 0 10px 2px rgba(0, 0, 0, 0.1);
      border-radius: 2px;
      padding: 0.45rem;

      &:hover {
        background: darken($button-bg-color, 4%);
      }

      &:active {
        background: $button-bg-color;
        box-shadow: inset 0 0 10px 2px rgba(0, 0, 0, 0.2);
      }
    }
  }
}
</style>
