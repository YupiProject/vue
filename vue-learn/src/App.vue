<template>
  
  <h1>Список дел</h1>
  <br>
  
  <Todo 
    v-for="todo in todos"
    :id="todo.id"
    :point="todo.point"
    :key="todo.id"
    @remove="remove"
    @change="change"
  />

  <TodoFrom 
    @add="add"
  />

</template>

<script>

import Todo from '../src/components/Todo.vue';
import TodoFrom from '../src/components/TodoFrom.vue';

export default {
  components: {
    Todo, TodoFrom
  },
  data() {
  return {
    todos: []
  }
 },
 methods:{
  remove(id) {
    this.todos = this.todos.filter((todo) => {
      return todo.id !== id;
    });
  },
  change(id,point){
    this.todo = this.todos.map((todo) => {
      if(todo.id === id){
        todo.point = point;
      }
      return todo;
    });
  },
  add(point){
    let id = this.todos.length + 1;

    this.todos.push({
      id,
      point
    });
  }
 }

}
</script>

<style>


  h1{
    height: 100px;
    text-align:center;
    font-size: 40px;  
  }
  
  body {
  height: 100vh;
  background: linear-gradient(90deg,#e52e71,#ff8a00);
  position: relative;
    
}

.slider-thumb::before {
  position: absolute;
  content: "";
  left: 30%;
  top: 20%;
  width: 450px;
  height: 450px;
  background: #17141d;
  border-radius: 62% 47% 82% 35% / 45% 45% 80% 66%;
  will-change: border-radius, transform, opacity;
  animation: sliderShape 5s linear infinite;
  display: block;
  z-index: -1;
  -webkit-animation: sliderShape 5s linear infinite;
}
@keyframes sliderShape{
  0%,100%{
  border-radius: 42% 58% 70% 30% / 45% 45% 55% 55%;
    transform: translate3d(0,0,0) rotateZ(0.01deg);
  }
  34%{
      border-radius: 70% 30% 46% 54% / 30% 29% 71% 70%;
    transform:  translate3d(0,5px,0) rotateZ(0.01deg);
  }
  50%{
    transform: translate3d(0,0,0) rotateZ(0.01deg);
  }
  67%{
    border-radius: 100% 60% 60% 100% / 100% 100% 60% 60% ;
    transform: translate3d(0,-3px,0) rotateZ(0.01deg);
  }
}
</style>