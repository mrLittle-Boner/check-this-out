<template>
  <ul class="view">
    <li class="view__title">List {{ id }}</li>
    <li
      v-for="(item,index) in items"
      class="view__item"
      :class="{'view__item--hide': !item.isSelected || item.count < 1}"
      :key="index"
    >
      <span 
        class="view__square"
        :style="{'background-color': item.color}" 
        v-for="n in item.count" :key="n"
        @click="$emit('deleteSquare', id,index)"
      ></span>
    </li>
  </ul>
</template>

<script>
export default {
  emits:['deleteSquare'],
  props: {
    id: {
      type:Number,
      required: true
    },
    items: {
      type: Array,
      required: true
    }
  },
}
</script>

<style scoped>
.view {
  border: 1px solid tomato;
  padding: 10px;
}

.view__item {
  background-color: #eee;
  display: flex;
  flex-wrap: wrap;
  gap: 4px;
  padding: 5px;
}

.view__square {
  width: 12px;
  height: 12px;
  display: inline-block;
  cursor: pointer;
}

.view__item--hide {
  display: none;
}

</style>