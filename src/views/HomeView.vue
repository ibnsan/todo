<template>
  <div>
    <h2>Create your to-do list</h2>
    <div>
      <input v-model="title" placeholder="Title"/>
      <input v-model="description" placeholder="Description"/>
      <button @click="createNewToDo">Create</button>
    </div>

    <div>
      <h3>Current to-do list</h3>
      <div v-for="todo in todoList" :key="todo.id">
        <p>Title: {{todo.title}}</p>
        <p>Description: {{todo.description}}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Create your to-do list',
  data() {
    return {
      title: '',
      description: '',
      todoList: []
    }
  },
  methods: {
    createNewToDo() {
      let test = {id: Date.now(), title: this.title, description: this.description}
      this.todoList.push(test);
      localStorage.setItem('todoList', JSON.stringify(this.todoList))
    }
  },
  mounted() {
    const currentTodoList = localStorage.getItem('todoList');
    if(currentTodoList && Array.isArray(currentTodoList)){
      this.todoList.push(localStorage.getItem('todoList'));
    }
  }
}
</script>
