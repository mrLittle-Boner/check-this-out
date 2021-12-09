<template>
  <div class="lists">
    <AList
      v-for="(list,index) in lists" :key="index"
      :listNumber="list.id" :items="list.items"
      @changeColor="changeColor"
    />
  </div>
  <div class="lists-view">
    <ul class="lists-view__list" v-for="list in lists" :key="list.id">
      <li class="list-view__title">List {{ list.id }}</li>
      <li class="lists-view__item" v-for="(item,index) in list.items" :key="index">
        <span class="list-view__square" :style="{'background-color': item.color}" v-for="(n) in item.count" :key="n"></span>
      </li>
    </ul>
  </div>  
</template>

<script>
import AList from './components/AList.vue'
import { ref } from 'vue'
export default {
  components: { AList },
  setup() {
    const lists = ref([
      {id:1, 
        items:[
          {count:4, color:'#ffffff'},
          {count:7, color:'#000000'},
          {count:12, color:'#ff00e1'},
          {count:5, color:'#00c9b2'},
          {count:2, color:'#333333'}
        ]
      }
    ])

    function changeColor(listId,itemInedx,newColor) {
      lists.value.map(list => {
        if(list.id === listId) {
          list.items[itemInedx].color = newColor
          console.log(listId,itemInedx,newColor)
        }
      })
    }

    return {
      lists,changeColor
    }
  },
}
</script>

<style>
*,*::after,*::before {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
ul {
  list-style-type: none;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  padding: 20px;

  display: flex;
  justify-content: space-between;
}
.lists,
.lists-view {
  border: 1px solid tomato;
  width: 40%;
  padding: 20px;
}

.lists-view__list {
  border: 1px solid tomato;
  padding: 10px;
}

.lists-view__item {
  background-color: #eee;
  display: flex;
  flex-wrap: wrap;
  gap: 4px;
  padding: 5px;
}
.list-view__square {
  width: 12px;
  height: 12px;
  display: inline-block;
  cursor: pointer;
}
</style>
