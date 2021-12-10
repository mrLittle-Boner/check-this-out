<template>
  <div class="list">
    <label class="list__title">
      <input
        class="list__checkbox"
        :class="{'list__checkbox--semicecked': !isAllItemsChecked && isSomeItemsChecked}"
        type="checkbox"
        :checked="isAllItemsChecked"
        @change="$emit('toggleAllItems', id)"
      >
      <h3>List {{ id }}</h3>
    </label>

    <ul class="list__items">
      <li class="list__item" v-for="(item,index) in items" :key="index">
        <label>
          <input
            type="checkbox"
            :checked="item.isSelected"
            @change="$emit('toggleItemSelect', id, index)"
          >
          <span>Item {{ index+1 }}</span>
        </label>
        <div class="list__item-controls">
          <span class="list__item-count">{{ item.count }}</span>
          <input
            class="list__item-newcount"
            type="number"
            min="1"
            required
            @change="(e) => $emit('changeCount', id, index, e.target.valueAsNumber)"
          >
          <input
            class="list__item-color"
            type="color"
            v-model="item.color"
            @change="(e) => $emit('changeColor', id, index, e.target.value)"
          >
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
import { computed } from '@vue/reactivity'

export default {
  emits:['changeColor', 'toggleItemSelect','changeCount', 'toggleAllItems'],
  props: {
    items: {
      type: Array,
      required: true
    },
    id: {
      type: Number,
      required: true
    }
  },
  setup(props){
    const isAllItemsChecked = computed(() => {
      return props.items.every(item => item.isSelected)
    })

    const isSomeItemsChecked = computed(() => {
      return props.items.some(item => item.isSelected)
    })

    return { isAllItemsChecked, isSomeItemsChecked }
  }
}
</script>

<style scoped>

.list__title {
  display: flex;
  gap: 25px;
  align-items: center;
  margin-bottom: 15px;
}
.list__items {
  list-style-type: none;
  margin-left: 35px;
}

.list__item {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.list__item-controls,
.list__item label {
  display: flex;
  align-items: center;
  gap: 8px;
}
.list__item-newcount {
  width: 40px ;
}
.list__item-newcount::-webkit-outer-spin-button,
.list__item-newcount::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}
.list__item-newcount[type=number] {
  -moz-appearance: textfield;
}

.list__checkbox {
  position: relative;
}

.list__checkbox--semicecked::before {
    position: absolute;
    top: 4px;
    left: 4px;
    width: 5px;
    height: 5px;
    content: " ";
    background-color: black;
}
</style>