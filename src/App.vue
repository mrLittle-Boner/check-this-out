<template>
  <div class="left">
    <ListControls
      v-for="(list,index) in lists" :key="index"
      :id="list.id" :items="list.items"
      @changeColor="changeColor"
      @toggleItemSelect="toggleItemSelect"
    />
  </div>

  <div class="right">
    <ListView
      v-for="list in lists" :key="list.id"
      :id="list.id"
      :items="list.items"
    />
  </div>  
</template>

<script>
import ListControls from './components/ListControls.vue'
import ListView from './components/ListView.vue'

import { ref } from 'vue'
export default {
  components: { ListControls, ListView },
  setup() {
    const lists = ref([
      {id:1, 
        items:[
          {count:4, color:'#ffffff', isSelected: true},
          {count:7, color:'#000000', isSelected: true},
          {count:12, color:'#ff00e1', isSelected: true},
          {count:5, color:'#00c9b2', isSelected: true},
          {count:2, color:'#333333', isSelected: true}
        ]
      }
    ])

    function changeColor(listId,itemInedx,newColor) {
      lists.value.map(list => {
        if(list.id === listId) {
          list.items[itemInedx].color = newColor
        }
      })
    }

    function toggleItemSelect(listId,itemInedx) {
      lists.value.map(list => {
        if(list.id === listId) {
          list.items[itemInedx].isSelected = !list.items[itemInedx].isSelected
        }
      })
    }

    return { lists, changeColor, toggleItemSelect }
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
.left,
.right {
  border: 1px solid tomato;
  width: 40%;
  padding: 20px;
}
</style>
