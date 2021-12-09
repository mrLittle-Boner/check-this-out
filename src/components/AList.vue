<template>
  <div class="list">
    <div class="list__title">
      <input type="checkbox">
      <h3>List {{ listNumber }}</h3>
    </div>

    <ul class="list__items">
      <li class="list__item" v-for="(item,index) in items" :key="index">
        <label>
          <input type="checkbox">
          <span>Item {{ index+1 }}</span>
        </label>
        <div class="list__item-controls">
          <span class="list__item-count">{{ item.count }}</span>
          <input
            class="list__item-color"
            type="color"
            v-model="item.color"
            @change="(e) => $emit('changeColor', listNumber,index, e.target.value)"
          >
        </div>
      </li>
    </ul>
  </div>
</template>

<script>

export default {
  emits:['changeColor'],
  props: {
    items: {
      type: Array,
      required: true
    },
    listNumber: {
      type: Number,
      required: true
    }
  },
  setup(){
    function showmeevent(e){
      console.log(e)
    }
    return { showmeevent }
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

</style>