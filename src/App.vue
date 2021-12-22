<template>
  <div class="left">
    <ListControls v-for="(n,i) in lists.length" :key="lists[i].id" v-model='lists[i]' />  
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
          {count:10, color:'#ffffff', isSelected: true},
          {count:10, color:'#0022ff', isSelected: true},
          {count:10, color:'#ff0015', isSelected: true},
          {count:5, color:'#00c9b2', isSelected: false},
          {count:2, color:'#333333', isSelected: false}
        ]
      },
      {id:2, 
        items:[
          {count:10, color:'#ff0015', isSelected: true},
          {count:10, color:'#ff6a00', isSelected: true},
          {count:10, color:'#ffe600', isSelected: true},
          {count:10, color:'#03ff20', isSelected: true},
          {count:10, color:'#170ceb', isSelected: true},
          {count:10, color:'#80007d', isSelected: true}
        ]
      },
      {id:3, 
        items:[
          {count:10, color:'#030bfc', isSelected: true},
          {count:10, color:'#030bfc', isSelected: true},
          {count:10, color:'#fff700', isSelected: true},
          {count:10, color:'#fff700', isSelected: true},
          {count:5, color:'#333333', isSelected: false}
        ]
      },
    ])

    function deleteSquare(listId,itemInedx) {
      const searchedList = lists.value.find(list => list.id === listId)
      searchedList.items[itemInedx].count--
    }
    
    return { lists, deleteSquare }
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
