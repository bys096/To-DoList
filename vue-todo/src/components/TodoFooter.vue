<template>
  <div class="clearAllContainer">
    <span class="clearAllBtn"
      @click="clearTodo()">Clear All</span>
  </div>
</template>

<script>
export default {
  methods: {
    clearTodo: function() {
      this.$emit('clearAll');
    }
  }
}
</script>

<style scoped>
.clearAllContainer {
  width: 8.5rem;
  height: 50px;
  line-height: 50px;
  background-color: white;
  border-radius: 5px;
  margin: 10px auto;
}
.clearAllBtn {
  color: #e20303;
  display: block;
  cursor: pointer;
}
</style>