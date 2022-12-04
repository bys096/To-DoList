<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <TodoInput v-on:addTodoItem="addOneItem"></TodoInput>
    <TodoList v-bind:propsdata="todoItems"
    v-on:removeItem="removeOneItem"></TodoList>
    <TodoFooter v-on:clearAll="clearAllItems"></TodoFooter>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoFooter from './components/TodoFooter.vue'
import TodoList from './components/TodoList.vue'
import TodoInput from './components/TodoInput.vue'



export default {
  data: function() {
    return {
      todoItems: []
    }
  },
  created: function() {
    if(localStorage.length > 0) {
      for(var i = 0; i < localStorage.length; i++) {
        // localStorage에 loglevel-webpack이 담겨있으므로 제외
        if(localStorage.key(i) !== "loglevel:webpack-dev-server"){
          // this.todoItems.push(localStorage.key(i));

          // JSON.stringify로 받은 String으로 변환한 객체를 다시 객체로 돌림
          this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
        }
      }
    }
  },
  
  components: {
    'TodoHeader' : TodoHeader,
    'TodoFooter' : TodoFooter,
    'TodoList' : TodoList,
    'TodoInput' : TodoInput,
    
  },

  methods: {
    addOneItem: function(todoItem) {
      var obj = {completed: false, item: todoItem};
        // localStorage.setItem()을 통해 저장 후, 초기화
        // localStorage.setItem(this.newTodoItem, this.newTodoItem);

        // 체크리스트의 완성여부를 위한 obj 객체 생성 후 JSON.stringify로 저장
        localStorage.setItem(todoItem, JSON.stringify(obj));
        this.todoItems.push(obj);
    },
    removeOneItem: function(todoItem, index) {
      localStorage.removeItem(todoItem);
      this.todoItems.splice(index, 1);
    },
    clearAllItems: function() {
      localStorage.clear();
      this.todoItems = [];
    }
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
  box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
}
</style>

