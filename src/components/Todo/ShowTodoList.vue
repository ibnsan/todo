<template>
  <div class="mx-auto lg:w-2/6 w-full">
    <div v-for="todo in todoList" :key="todo.id" class="bg-gray-100 rounded flex p-4 h-full  flex flex-col md:mt-5">
      <span class="title-font">Title: {{ todo.title }}</span>
      <span class="title-font">Description: {{ todo.description }}</span>
      <span class="title-font">Project: {{ todo.project }}</span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    todoList: {
      type: Array,
      required: true
    }
  }
}
</script>