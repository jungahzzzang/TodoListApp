<template>
  <div id="app" class="container">
    <h1 class="text-center">Todo App</h1>
    <input type="text" class="w-100 p-2" placeholder="Type todo" @keyup.enter="addTodo"
    v-model="todoText">
    <hr>
   <Todo v-for="todo in todos" :key="todo.id" :todo="todo" @toggle-checkbox="toggleCheckbox" @click-delete="deleteTodo"/>
    {{todos}}
  </div>
</template>

<script>
import Todo from '@/components/Todo.vue';

export default {
  components:{
    Todo
  },
  data(){
    return {
      todoText: '',
      todos: [
        { id: 1, text: 'buy a car', checked: false},
        { id: 2, text: 'play game', checked: false},
      ]
    }
  },

  methods:{
    deleteTodo(id){
      const index = this.todos.findIndex(todo=>{
        return todo.id === id;
      });
      this.todos.splice(index,1);
      //this.todos = this.todos.filter(todo=>todo.id !== id);
    },
    addTodo(e){
      //console.log(e.target.value)
      this.todos.push({
        id: Math.random(),  //원래는 DB값이지만 DB가 없으므로 Math.random() 사용
         text: e.target.value,
         checked: false
      });
      this.todoText = '';
    },
    toggleCheckbox({id, checked}){
      //console.log(id, checked)
      const index = this.todos.findIndex(todo=>{
        return todo.id === id;  
      });
      this.todos[index].checked = checked;
    }
  }
}
</script>

