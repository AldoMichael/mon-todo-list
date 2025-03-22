<template>
  <button @click="triTodoList">Reorganise</button>
  <form action="" @submit.prevent="ajoutList">
  <p>Eto ilay test page</p>
  <input type="text" v-model="listTodo.title">{{ listTodo.title }}
  <button>Click</button><hr>
  <div v-if="todoLists.length > 0">
    <ul v-for="(todoList, index) in todoLists" :key="index">
      <li>
        <input type="checkbox" v-model="todoList.completed" :id="'check-' + index" @click="Completed(index)">
            <span :class="{barre: todoList.completed}">{{todoList}}</span>
        <button @click="suppList(index)">Supprimer</button>
      </li>
    </ul>
  </div>
  <div v-else>
    <p>Tsy misy list ny zavatra atao</p>
  </div>
</form>
</template>

<script setup>
import { ref } from 'vue'

const listTodo = ref([{title:'', completed: false, date: new Date()}]);
//const checkList = ref([]);
const todoLists = ref([]);

const ajoutList = () =>{
  if(listTodo.value.title){
    alert(listTodo.value.title, listTodo.value.title);
    todoLists.value.push({
      title: listTodo.value.title, 
      completed : false, 
      date: new Date()});
    listTodo.value.title = "";
  }
  else{
    alert("Input list vide");
  }
}

const suppList = (index) =>{
  if(confirm("Tena ho fafana ny Lisy " + index))
  {
    todoLists.value.splice(index, 1);
  }
}

const Completed = (index) => {
  todoLists.value[index].completed = !todoLists.value[index].completed;
}

const triTodoList = () => {
  todoLists.value.sort((a, b) => a.completed - b.completed);
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
