<template>
  <div>
    <div class="mx-auto lg:w-2/6 md:w-1/2 bg-gray-100 rounded-lg p-8 flex flex-col w-full mt-10 md:mt-0">
      <h2 class=" mx-auto text-gray-900 text-lg font-medium title-font mb-5">Choose the project</h2>
      <choose-project :project-list="projectList" @selectedProject="setCurrentProject"/>

      <h2 class=" mx-auto text-gray-900 text-lg font-medium title-font mb-5">Or create a new project</h2>
      <create-project :project-list="projectList" @savedProjects="updateProjectList"/>

      <h2 class="mx-auto text-gray-900 text-lg font-medium title-font mb-5">Create your to-do list</h2>
      <create-todo :name-selected-project="nameSelectedProject" @savedTodo="updateTodoList"/>
    </div>
    <show-todo-list :todo-list="todoList"/>
  </div>
</template>

<script>

import ChooseProject from "@/components/Project/ChooseProject";
import CreateProject from "@/components/Project/CreateProject";
import CreateTodo from "@/components/Todo/CreaeTodo";
import ShowTodoList from "@/components/Todo/ShowTodoList";

export default {
  name: 'home-page',
  components: {ShowTodoList, CreateTodo, CreateProject, ChooseProject},
  data() {
    return {
      nameSelectedProject: '',
      todoList: [],
      projectList: [],
    }
  },
  methods: {
    setCurrentProject(name) {
      this.nameSelectedProject = name;
    },
    updateProjectList(selectedProject) {
      this.nameSelectedProject = selectedProject.name;
      this.projectList.push(selectedProject);
    },
    updateTodoList(newTodo) {
      this.todoList.push(newTodo);
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
