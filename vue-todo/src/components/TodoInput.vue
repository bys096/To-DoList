
<template>
<div class="inputBox shadow">
  <!-- Enter가 눌리면 addTodo 메서드 실행 -->
  <input type="text" v-model="newTodoItem" @keyup.enter="addTodo">
  <!-- <button @click="addTodo">add</button> -->
  <span class="addContainer" @click="addTodo">
    <i class="fa-solid fa-plus addBtn"></i>
  </span>

  <Modal v-if="showModal" @close="showModal = false">
    <!--
      you can use custom content here to overwrite
      default content
    -->
    <h3 slot="header">
      경고!
      <i class="fa-solid fa-delete-left closeModalBtn" @click="showModal=false"></i>
    </h3>

    <h3 slot="body"> 무언가를 입력하세요.</h3>

    <!-- <div slot="footer"> copy right</div> -->
    <div slot="footer">
      
    </div>
  </Modal>
</div>
</template>

<script>
import Modal from './common/Modal.vue'
export default {
  data: function() {
    return {
      newTodoItem: "",
      showModal: false
    }
  },
  methods: {
    addTodo: function() {
      if(this.newTodoItem !== '') {
        this.$emit('addTodoItem', this.newTodoItem);
        this.clearInput();
      } else {
        this.showModal = !this.showModal;
      }

      
    },
    clearInput: function() {
      this.newTodoItem = '';
    }
  },
  components: {
    Modal: Modal
  }
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
  cursor: pointer;
}
.addBtn {
  color: white;
  vertical-align: middle;
}
.closeModalBtn {
  color: #42b983;
  /* color: black; */
  position: relative;
  left: 120px;
}
</style>