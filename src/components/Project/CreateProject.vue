<template>
  <div class="relative mb-4">
    <todo-input v-model="projectName" placeholder="Project name"/>
  </div>
  <todo-button @click="createNewProject">Create</todo-button>
</template>

<script>
export default {
  name: 'create-project',
  emits: ["savedProjects"],
  props: {
    projectList: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      projectName: '',
      nameSelectedProject: '',
    }
  },
  methods: {
    createNewProject() {
      if (this.projectName.length >= 3) {
        const newProject = {id: Date.now(), name: this.projectName, value: this.projectName, status: 'backLog'};
        this.$emit('savedProjects', newProject);
        localStorage.setItem('projectList', JSON.stringify(this.projectList));
      }
    },
  }
}
</script>