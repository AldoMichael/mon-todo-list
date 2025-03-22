<template>
  <form action="" @submit.prevent="ajoutList">
  <p>Eto ilay test page</p>
  <input type="text" v-model="listTodo.title">{{ listTodo.title }}
  <button>Click</button><hr>
  <button @click="triTodoList">Reorganise</button>
  <div v-if="todoLists.length > 0">
    <ul v-for="(todoList, index) in todoLists" :key="index">
      <li>
        <input type="checkbox" v-model="checkList[index]" :id="'check-' + index">
            <span :class="{barre: checkList[index]}">{{todoList}}</span>
        <button @click="suppList(index)">Supprimer</button>
      </li>
      {{ checkList[index] }}
    </ul>
  </div>
  <div v-else>
    <p>Tsy misy list ny zavatra atao</p>
  </div>
</form>
</template>

<script setup>
import { ref } from 'vue'

const listTodo = ref([{title:'', completed: false, date: new Date()}])
const checkList = ref([])
const todoLists = ref([{title:'', completed: false, date: new Date()}])

const ajoutList = () =>{
  if(listTodo.value.title){
    alert(listTodo.value.title, listTodo.value.title)
    console.log('listTodo---->', listTodo.value)
    todoLists.value.push({title: listTodo.value.title, completed : checkList.value, date: new Date()})
    console.log('todoLists---->', todoLists.value)
    listTodo.value.title = "";
  }
  else{
    alert("Input list vide")
  }
}

const suppList = (index) =>{
  if(confirm("Tena ho fafana ny Lisy " + index))
  {
    //todoLists.index = todoLists.index.filter(i => i !== index)
    todoLists.value.splice(index, 1);
  }
}

const triTodoList = () => {
  todoLists.value.sort((a, b) => a > b ? 1 : -1)
  checkList.value.sort((a, b) => a - b ? 1 : -1)
}

</script>

<style>
.barre {
  position: relative;
  color: "#adabab";
}

.barre::after {
  content: "";
  position: absolute;
  left: 0;
  top: 50%;  /* Place la ligne au milieu */
  width: 100%;
  height: 2px; /* Épaisseur de la ligne */
  background: red; /* Couleur personnalisée */
  transform: translateY(-50%);
}
</style>
