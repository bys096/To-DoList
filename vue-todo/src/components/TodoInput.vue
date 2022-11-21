
<template>
<div class="inputBox shadow">
  <!-- Enter가 눌리면 addTodo 메서드 실행 -->
  <input type="text" v-model="newTodoItem" @keyup.enter="addTodo">
  <!-- <button @click="addTodo">add</button> -->
  <span class="addContainer" @click="addTodo">
    <i class="fa-solid fa-plus addBtn"></i>
  </span>
</div>
</template>

<script>
export default {
  data: function() {
    return {
      newTodoItem: ""
    }
  },
  methods: {
    addTodo: function() {
      console.log(this.newTodoItem);
      // localStorage.setItem()을 통해 저장 후, 초기화
      localStorage.setItem(this.newTodoItem, this.newTodoItem);
      this.clearInput();
    },
    clearInput: function() {
      this.newTodoItem = '';
    }
  },
}
</script>

<style scoped>
input:focus {
  outline: none;
}
.inputBox {
  background: white;
  height: 50px;
  line-height: 50px;
  border-radius: 5px;
}
.inputBox input {
  border-style: none;
  font-size: 0.9rem;
}
.addContainer {
  float: right;
  background: linear-gradient(to right, #6478FB, #8773FB);
  display: block;
  width: 3rem;
  border-radius: 0 5px 5px 0;
}
.addBtn {
  color: white;
  vertical-align: middle;
}

</style>