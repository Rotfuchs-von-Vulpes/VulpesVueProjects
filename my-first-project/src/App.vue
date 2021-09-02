<template>
  <div id="app">
    <h1>Welcome to Vulpes Todo</h1>
    <to-do
      v-for="(toDo, key) in list"
      v-bind:key="key"
      :todo="toDo.name"
      :nestedToDoList="toDo.nestedToDoList"
      @delete="deleteToDo(key)"
    />
    <new-to-do @submit="addToDo"  />
  </div>
</template>

<script>
import NewToDo from "./components/NewToDo.vue";
import ToDo from "./components/ToDoComponent.vue";

if (!localStorage.getItem('list')) {
  let doc = [];

  localStorage.setItem('list', JSON.stringify(doc));
}

export default {
  name: "App",
  components: {
    ToDo,
    NewToDo,
  },
  methods: {
    updateLocalStorage: function() {
      localStorage.setItem('list', JSON.stringify(this.list));
    },
    addToDo: function(toDo) {
      this.newToDo = {
        name: '',
        nestedToDoList: [
          {
            checked: false,
            description: ''
          }
        ]
      }
      this.list.push(toDo);
      this.updateLocalStorage();
    },
    deleteToDo: function(idx) {
      this.list.splice(idx, 1);
      this.updateLocalStorage(this.list);
    }
  },
  data() {
    return {
      list: JSON.parse(localStorage.getItem('list')),
      newToDo: {
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
};
</script>

<style>
* {
  background-color: #050d14;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #5f7792;
  margin-top: 60px;
}
</style>
