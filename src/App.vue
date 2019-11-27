<template>
  <div id="app">
    <TodoHeaderVue></TodoHeaderVue>
    <TodoInputVue v-on:addTodoItem="addOneItem"></TodoInputVue>
    <TodoListVue v-bind:propsdata="todoItems" @removeTodo="removeOneItem" @toggleItem="toggleOneItem"></TodoListVue>
    <TodoFooterVue v-on:removeAll="clearAll"></TodoFooterVue>
  </div>
</template>

<script>
import TodoHeaderVue from "./components/TodoHeader.vue";
import TodoInputVue from "./components/TodoInput.vue";
import TodoListVue from "./components/TodoList.vue";
import TodoFooterVue from "./components/TodoFooter.vue";

export default {
  data() {
    return {
      todoItems: []
    }
  },
  created() {
    if(localStorage.length > 0){
      for (var i=0; i < localStorage.length; i++){
        if(localStorage.key(i) !== 'loglevel:webpack-dev-server'){
          this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
          
        }
        
      }
    }
  },
  methods: {
    addOneItem(todoItem) {
      var obj = {completed:false, item: todoItem};
      localStorage.setItem(todoItem, JSON.stringify(obj));
      this.todoItems.push(obj);
    },
    clearAll(){
      localStorage.clear();
      this.todoItems = [];
    },
    removeOneItem(todoItem,index){      
      localStorage.removeItem(todoItem.item);
      this.todoItems.splice(index,1);
    },
    toggleOneItem(todoItem,index) {
      todoItem.completed = !todoItem.completed;
      // this.todoItem[index].completed = !this.todoItem[index].completed;
      localStorage.removeItem(todoItem.item);
      localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
    },
  },
  components: {
    TodoHeaderVue,
    TodoInputVue,
    TodoListVue,
    TodoFooterVue
  }
};
</script>

<style>
body {
  text-align: center;
  background-color: #f6f6f8;
}
</style>
