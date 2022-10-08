<template>
  <div>
    <div class="mx-auto lg:w-2/6 md:w-1/2 bg-gray-100 rounded-lg p-8 flex flex-col w-full mt-10 md:mt-0">
      <h2 class=" mx-auto text-gray-900 text-lg font-medium title-font mb-5">Create your to-do list</h2>
      <div class="relative mb-4">
        <input v-model="title" type="text" placeholder="Title" name="Title"
               class="w-full bg-white rounded border border-gray-300 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 text-base outline-none text-gray-700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out">
      </div>
      <div class="relative mb-4">
        <textarea v-model="description" placeholder="Description" name="description"
                  class="w-full bg-gray-100 bg-opacity-50 rounded border border-gray-300 focus:border-indigo-500 focus:bg-white focus:ring-2 focus:ring-indigo-200 h-32 text-base outline-none text-gray-700 py-1 px-3 resize-none leading-6 transition-colors duration-200 ease-in-out"></textarea>
      </div>
      <button class="text-white bg-indigo-500 border-0 py-2 px-8 focus:outline-none hover:bg-indigo-600 rounded text-lg"
              @click="createNewToDo">Create
      </button>
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
      if (this.title.length >= 3 && this.description.length >= 3) {
        let test = {id: Date.now(), title: this.title, description: this.description}
        this.todoList.push(test);
        localStorage.setItem('todoList', JSON.stringify(this.todoList));
      }
    }
  },
  mounted() {
    const currentTodoList = JSON.parse(localStorage.getItem('todoList'));
    if (currentTodoList && Array.isArray(currentTodoList)) {
      this.todoList = currentTodoList;
    }
  }
}
</script>
