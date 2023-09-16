<template>
  <form class="form" @submit.prevent="addItem">
    <input
      type="text"
      class="form__input"
      placeholder="Input here..."
      v-model="itemText" />
    <button @click="addItem" type="button" class="form__btn form__btn--primary">
      Add
    </button>
  </form>
</template>

<script lang="ts">
import { Item } from '@/types/types';
import { defineComponent } from 'vue';

interface State {
  itemText: string;
}

export default defineComponent({
  data(): State {
    return {
      itemText: '',
    };
  },

  methods: {
    addItem() {
      this.$emit('addItem', {
        id: Date.now().toString(),
        text: this.itemText,
        completed: false,
      });
      this.itemText = '';
    },
  },
  emits: {
    addItem: (item: Item) => item,
  },
});
</script>

<style lang="scss">
@import '../assets/styles/variables.scss';
.form {
  display: flex;
  margin-right: 2rem;

  @media screen and (max-width: 720px) {
    margin-right: 0;
  }

  &__input {
    width: 420px;
    background: #fff;
    color: $input-text-color;
    font: inherit;
    box-shadow: 0 6px 10px 0 rgba(0, 0, 0, 0.1);
    border: 0;
    outline: 0;
    padding: 0.75rem;

    @media screen and (max-width: 720px) {
      width: 300px;
    }

    @media screen and (max-width: 480px) {
      width: 260px;
    }
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
