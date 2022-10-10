<template>
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
      this.$emit('selectedProject', this.projectName);
    }
  }
}
</script>