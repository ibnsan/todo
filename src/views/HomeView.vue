<template>
  <div>

    <div class="mx-auto lg:w-2/6 md:w-1/2 bg-gray-100 rounded-lg p-8 flex flex-col w-full mt-10 md:mt-0">
      <h2 class=" mx-auto text-gray-900 text-lg font-medium title-font mb-5">Choose the project</h2>
      <div class="relative mb-4">
        <todo-select v-model="projectName" :options="projectList" />
        {{projectName}}
      </div>
      <h2 class=" mx-auto text-gray-900 text-lg font-medium title-font mb-5">Or create a new project</h2>

      <div class="relative mb-4">
        <todo-input v-model="projectName" placeholder="Project name"/>
      </div>
        <todo-button @click="createNewProject">Create</todo-button>


      <h2 class="mx-auto text-gray-900 text-lg font-medium title-font mb-5">Create your to-do list</h2>
      <div class="relative mb-4">
        <todo-input v-model="title" placeholder="Title"/>
      </div>
      <div class="relative mb-4">
        <todo-textarea v-model="description" placeholder="Description"/>
      </div>
      <todo-button @click="createNewToDo">Create</todo-button>
    </div>

    <div class="mx-auto lg:w-2/6 w-full">
      <div v-for="todo in todoList" :key="todo.id" class="bg-gray-100 rounded flex p-4 h-full  flex flex-col md:mt-5">
        <span class="title-font">Title: {{ todo.title }}</span>
        <span class="title-font">Description: {{ todo.description }}</span>
      </div>
    </div>
  </div>
</template>

<script>
import TodoButton from "@/components/UI/buttons/TodoButton";
import TodoInput from "@/components/UI/inputs/TodoInput";
import TodoTextarea from "@/components/UI/TodoTextarea";
import TodoSelect from "@/components/UI/TodoSelect";
export default {
  name: 'Create your to-do list',
  components: {TodoSelect, TodoTextarea, TodoInput, TodoButton},
  data() {
    return {
      title: '',
      description: '',
      projectName: '',
      todoList: [],
      projectList: [],
    }
  },
  methods: {
    createNewToDo() {
      if (this.title.length >= 3 && this.description.length >= 3) {
        this.todoList.push({id: Date.now(), title: this.title, description: this.description});
        localStorage.setItem('todoList', JSON.stringify(this.todoList));
      }
    },
    createNewProject() {
      if (this.projectName.length >= 3) {
        this.projectList.push({id: Date.now(), name: this.projectName, value: this.projectName});
        localStorage.setItem('projectList', JSON.stringify(this.projectList));
      }
    }
  },
  mounted() {
    const currentProjectList = JSON.parse(localStorage.getItem('projectList'));
    if (currentProjectList && Array.isArray(currentProjectList)) {
      this.projectList = currentProjectList;
    }
  }
}
</script>
