<template>
  <div class="Todo">
    <h2>{{ todo }}</h2>
    <div>
      <nested-to-do 
        v-for="(nestedToDo, key) in nestedToDoList" 
        v-bind:key="key" 
        :description="nestedToDo.description"
      />
      <input
        type="button"
        value="completar"
        @click="$emit('delete')"
      >
    </div>
  </div>
</template>

<script>
import NestedToDo from './NestedToDo.vue';

export default {
  name: 'ToDo',
  components: {
    NestedToDo
  },
  props: {
    todo: String,
    nestedToDoList: Array,
  }
}
</script>

<style scoped>
.Todo {
  border: 2px solid #5f7792;
  margin: 10px;
  padding: 20px;
}

input {
  border: 2px solid #5f7792;
  margin: 10px;
  color: #5f7792
}

input:active {
  border: 2px solid #b4ca34;
  color: #b4ca34;
}
</style>