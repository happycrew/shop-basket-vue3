<script lang="ts">
import { PropType, defineComponent } from 'vue';
import { Item } from '../types/types';
export default defineComponent({
  props: {
    basketItems: {
      type: Array as PropType<Item[]>,
    },
  },
});
</script>

<template>
  <ul class="list">
    <li class="list__item" v-for="(item, id) in basketItems" :key="item.id">
      <span :class="{ 'list__item-done': item.completed }">
        {{ id + 1 }}. {{ item.text }}
      </span>
      <button class="list__btn">Done</button>
    </li>
  </ul>
</template>

<style lang="scss">
@import '../assets/styles/variables.scss';

.list {
  list-style-type: none;
  &__item {
    font-size: 2em;
    text-align: left;
    display: flex;
    justify-content: space-between;
    margin-bottom: 5px;

    &-number {
      margin-right: 15px;
    }

    &-done {
      text-decoration: line-through;
      opacity: 0.6;
    }
  }
  &__btn {
    align-self: center;
    background: $button-done-bg-color;
    color: $button-text-color;
    box-shadow: 0 0 10px 2px rgba(0, 0, 0, 0.1);
    border-radius: 2px;
    padding: 0.65rem;
    height: 35px;
    border: 0;
    text-transform: uppercase;
    transition: all 200ms ease-in;
    cursor: pointer;

    &:hover {
      background: darken($button-done-bg-color, 8%);
    }

    &:active {
      background: $button-done-bg-color;
      box-shadow: inset 0 0 10px 2px rgba(0, 0, 0, 0.2);
    }
  }
}
</style>
