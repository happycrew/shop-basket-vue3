<script lang="ts">
import { PropType, defineComponent } from 'vue';
import { Item } from '../types/types';
export default defineComponent({
  props: {
    basketItems: {
      type: Array as PropType<Item[]>,
    },
  },
  methods: {
    toggleItem(id: string) {
      this.$emit('toggleItem', id);
    },
    removeItem(id: string) {
      this.$emit('removeItem', id);
    },
  },
});
</script>

<template>
  <ul v-if="basketItems?.length !== 0" class="list">
    <li class="list__item" v-for="(item, id) in basketItems" :key="item.id">
      <span class="list__item-content" :class="{ 'list__item-done': item.completed }">
        {{ id + 1 }}. {{ item.text }}
      </span>
      <div class="list__item-btns">
        <button @click="toggleItem(item.id)" class="list__btn list__btn-done">
          Done
        </button>
        <button @click="removeItem(item.id)" class="list__btn list__btn-remove">
          Remove
        </button>
      </div>
    </li>
  </ul>
  <h1 class="empty" v-else>Basket is empty</h1>
</template>

<style lang="scss">
@import '../assets/styles/variables.scss';

.empty {
  margin-top: 25%;
  @media screen and (max-width: 520px) {
    font-size: 1.3rem;
  }
}

.list {
  list-style-type: none;
  &__item {
    text-align: left;
    display: flex;
    justify-content: space-between;
    margin-bottom: 7px;

    &-content {
      font-size: 1.2em;
      width: 60%;
      word-break: break-all;
      align-self: center;
      @media screen and (max-width: 480px) {
        font-size: 0.9em;

      }
    }

    &-btns {
      display: flex;
      gap: 5px;
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

    @media screen and (max-width: 480px) {
      height: 25px;
      padding: 0.45px;
      font-size: 0.7rem;
    }

    &-done {
      background: $button-done-bg-color;

      &:hover {
        background: darken($button-done-bg-color, 8%);
      }

      &:active {
        background: $button-done-bg-color;
        box-shadow: inset 0 0 10px 2px rgba(0, 0, 0, 0.2);
      }
    }

    &-remove {
      background: $button-remove-bg-color;

      &:hover {
        background: darken($button-remove-bg-color, 8%);
      }

      &:active {
        background: $button-remove-bg-color;
        box-shadow: inset 0 0 10px 2px rgba(0, 0, 0, 0.2);
      }
    }
  }
}
</style>
