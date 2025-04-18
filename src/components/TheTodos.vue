<script setup>
import { reactive, ref } from 'vue'

const todoText = ref('')
const todos = reactive([
  {
    id: 1,
    text: 'buy milk',
    done: false,
  },
  {
    id: 2,
    text: 'buy bread',
    done: true,
  },
])

const addTodo = () => {
  // if not todo text return
  if (!todoText.value.trim()) return
  // add text to todos
  todos.push({
    id: todos.length + 1,
    text: todoText.value,
    done: false,
  })


  todoText.value = ''
}

</script>
<template>
  <div>
    <form @submit.prevent="addTodo" class="max-w-lg my-5 m-auto">
      <div class="flex item-center rounded-2xl border overflow-hidden">
        <input class="flex-1 b-0 py-2.5 px-3.5 outline-0" type="text" placeholder="add todo" v-model="todoText" />
        <button class="px-3.5 py-2.5 border-0 text-white bg-blue-600" type="submit">add</button>
      </div>
    </form>
    <ul class="list-none max-w-lg mt-5 mb-5 m-auto">
      <li class="flex items-center justify-between p-4 border-b-1 border-gray-300" v-for="todo in todos" :key="todo.id">
        <p :class="{' strikethrough': !todo.done}">{{ todo.text }}</p>
        <input type="checkbox" v-model="todo.done" />
      </li>
    </ul>
  </div>
</template>

<style>
.strikethrough {
  text-decoration: line-through;
  /* display: none; */
}
</style>
