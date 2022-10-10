<template>
  <div class="relative mb-4">
    <todo-input v-model="title" placeholder="Title"/>
  </div>
  <div class="relative mb-4">
    <todo-textarea v-model="description" placeholder="Description"/>
  </div>
  <todo-button @click="createNewToDo">Create</todo-button>
</template>

<script>
export default {
  name: 'create-todo',
  emits: ["savedTodo"],
  props: {
    nameSelectedProject: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      title: '',
      description: '',
    }
  },
  methods: {
    createNewToDo() {
      if (this.title.length >= 3 && this.description.length >= 3 && this.nameSelectedProject) {
        const newTodo = {id: Date.now(), title: this.title, description: this.description, project: this.nameSelectedProject};
        this.$emit('savedTodo', newTodo);
        localStorage.setItem('todoList', JSON.stringify(newTodo));
      }
    },
  }
}
</script>