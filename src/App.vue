<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <TodoInput v-on:addTodo="addTodo"></TodoInput>
    <TodoList v-bind:propsdata="todoItems" @removeTodo="removeTodo"></TodoList>
    <TodoFooter v-on:removeAll="clearAll"></TodoFooter>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoList   from './components/TodoList.vue'
import TodoInput  from './components/TodoInput.vue'
import TodoFooter from './components/TodoFooter.vue'

export default {
  data(){
    return {
      todoItems: [] // 데이터 속성 선언2
    }
  },

  created(){
        if (localStorage.length > 0) {
            for (var i = 0; i < localStorage.length; i++) {
              if(localStorage.key(i) !== 'loglevel:webpack-dev-server') {
                this.todoItems.push(JSON.parse(localStorage.getItem(key(i))));
              }
            }
        }
    },

  methods:{
    addTodo(todoItem) {
       var obj = {completed: false, item: todoItem};
       localStorage.setItem(todoItem, JSON.stringify(obj));
       this.todoItems.push(obj);
       console.log("add = "+ todoItem);
    },

    clearAll() {
      localStorage.clear();
      this.todoItems = [];
    },

    removeTodo(todoItem, index){
        localStorage.removeItem(todoItem);
        this.todoItems.splice(index, 1);

    }
  },


  components: {
    'TodoHeader'  : TodoHeader,
    'TodoList'    : TodoList,
    'TodoInput'   : TodoInput,
    'TodoFooter'  : TodoFooter,

  }
}


</script>

<style>
  body {
        text-align: center;
        background-color: #f6f6f6;
    }

    input {
        border-style: groove;
        width: 200px;
    }

    button {
        border-style: groove;
    }

    .shadow {
        box-shadow: 5px 10px 10px rgba(0,0,0,0.03)
    }
</style>
