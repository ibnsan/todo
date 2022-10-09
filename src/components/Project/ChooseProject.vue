<template>
  <h2 class=" mx-auto text-gray-900 text-lg font-medium title-font mb-5">Choose the project</h2>
  <div class="relative mb-4">
    <todo-select v-model="projectName" @update:model-value="setSelectedValue" :options="projectList" />
  </div>
</template>

<script>
import TodoSelect from "@/components/UI/TodoSelect";

export default {
  name: 'choose-project',
  components: {TodoSelect},
  props: {
    projectList : {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      projectName: '',
    }
  },
  methods: {
    setSelectedValue() {
      this.$emit('select', this.projectName);
    }
  }
}
</script>