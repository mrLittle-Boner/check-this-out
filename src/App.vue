<template>
  <div class="left">
    <ListControls
      v-for="(list,index) in lists" :key="index"
      :id="list.id" :items="list.items"
      @changeColor="changeColor"
      @toggleItemSelect="toggleItemSelect"
      @changeCount="changeCount"
      @toggleAllItems="toggleAllitems"
    />
  </div>

  <div class="right">
    <ListView
      v-for="list in lists" :key="list.id"
      :id="list.id"
      :items="list.items"
      @deleteSquare="deleteSquare"
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
      },
    ])

    function changeColor(listId,itemInedx,newColor) {
      lists.value.map(list => {
        if(list.id === listId) {
          list.items[itemInedx].color = newColor
        }
      })
    }

    function changeCount(listId,itemInedx,newCount){
      if(newCount < 0) {
        alert("New value should be more or equal to 0")
      }
      else {
        lists.value.map(list => {
          if(list.id === listId) {
            list.items[itemInedx].count = newCount
          }
        })
      }
    }

    function toggleItemSelect(listId,itemInedx) {
      lists.value.map(list => {
        if(list.id === listId) {
          list.items[itemInedx].isSelected = !list.items[itemInedx].isSelected
        }
      })
    }

    function deleteSquare(listId,itemInedx) {
      lists.value.map(list => {
        if(list.id === listId) {
          list.items[itemInedx].count--
        }
      })
    }

    function toggleAllitems(listId){
      lists.value.map(list => {
        const isAllItemsSelected = list.items.every(item => item.isSelected)
        console.log(isAllItemsSelected)
        if(list.id === listId && isAllItemsSelected) {
          list.items.map(item => item.isSelected = false)
        }
        if(list.id === listId && !isAllItemsSelected) {
          list.items.map(item => item.isSelected = true)
        }
      })
    }

    return { lists, changeColor, toggleItemSelect, deleteSquare, changeCount, toggleAllitems }
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
