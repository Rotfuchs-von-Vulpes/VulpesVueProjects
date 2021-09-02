<template>
  <div class="Newtodo">
    <form>
      <label>Nome:</label><br>
      <input type="text" v-model="name"><br>
      <label>Nome da nested to do</label><br>
      <li 
        v-for="(nestedToDo, key) in nestedToDoList"
        v-bind:key="key"
      >{{ nestedToDo.description }}</li>
      <input 
        type="text" 
        v-model="nestedToDoList[nestedToDoList.length - 1].description"
      ><br>
      <input 
        type="button" 
        @click="addNestedToDo()" 
        value="Adicionar Nested To Do"
      ><br>
      <input 
        type="button" 
        @click="addToDo()"
        value="Adicionar"
      >
    </form>
  </div>
</template>

<script>
export default {
  name: 'NewTodo',
  methods: {
    addNestedToDo: function() {
      this.nestedToDoList.push({
        checked: false,
        description: ''
      });
    },
    addToDo: function() {
      let todo = { name: this.name, nestedToDoList: this.nestedToDoList };
      
      this.$emit('submit', todo);
      this.name = '';
      this.nestedToDoList = [
        {
          checked: false,
          description: ''
        }
      ];
    }
  },
  data() {
    return {
      name: '',
      nestedToDoList: [
        {
          checked: false,
          description: ''
        }
      ]
    }
  }
}
</script>

<style scoped>
.Newtodo {
  border: 2px solid #5f7792;
  margin-left: 20px;
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