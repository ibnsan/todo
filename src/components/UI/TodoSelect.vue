<template>
    <div class="relative">
      <select :value="modelValue" @change="changeOption" class="w-full rounded border appearance-none border-gray-300 py-2 focus:outline-none focus:ring-2 focus:ring-indigo-200 focus:border-indigo-500 text-base pl-3 pr-10">
        <option disabled value="" selected>{{ disabledText }}</option>
        <option
            v-for="option in options"
            :key="option.id"
            :value="option.value"
        >
          {{ option.name }}
        </option>
      </select>
      <span class="absolute right-0 top-0 h-full w-10 text-center text-gray-600 pointer-events-none flex items-center justify-center">
        <svg fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
             class="w-4 h-4" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" d="M19.5 8.25l-7.5 7.5-7.5-7.5"/>
        </svg>
      </span>
    </div>
</template>

<script>
export default {
  name: 'todo-select',
  props: {
    modelValue: {
      type: String
    },
    options: {
      type: Array,
      default: () => []
    },
    disabledText: {
      type: String,
      default: 'Select from the list'
    }
  },
  methods: {
    changeOption(event) {
      this.$emit('update:modelValue', event.target.value);
    }
  }
}
</script>