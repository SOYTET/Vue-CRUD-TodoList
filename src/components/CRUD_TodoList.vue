
<template>
  <div>
    <form
      @submit.prevent="addTodo"
      class="mb-4 flex items-center justify-center"
    >
      <input
        v-model="newTodo"
        class="border-2 border-gray-400 p-2 rounded-md mr-2 focus:outline-none focus:border-blue-500 text-center"
      />
      <button
        class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
      >
        Add Todo
      </button>
    </form>
    <ul class="flex flex-wrap">
      <li v-for="todo in todos" :key="todo.id" class="w-full sm:w-1/2 p-4">
        <div
          class="bg-gray-100 rounded-md p-4 mb-2 flex justify-between items-center"
        >
          <div>
            <p class="mr-4">{{ todo.id }}</p>
            <p>{{ todo.text }}</p>
            <p v-if="todo.timestamp" class="text-xs text-gray-500">
              {{ todo.timestamp }}
            </p>
          </div>
          <div>
            <button
              @click="updateTodoText(todo, todo.text)"
              class="bg-green-500 hover:bg-green-700 text-white font-bold py-2 px-4 rounded mr-2"
            >
              Update
            </button>
            <button
              @click="removeTodo(todo)"
              class="bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 rounded"
            >
              Delete
            </button>
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>
<script setup>
import { ref } from "vue";

// A counter to generate unique IDs for todos
let id = 0;
let temID = 0;

// Refs for managing todos
const newTodo = ref("");
const todos = ref([
  { id: id++, text: "Final Exam in Semester I" },
  { id: id++, text: "Cook for Friends Tonight" },
  { id: id++, text: "Finish School project" },
]);


// Add todo function
let isUpdate = false;
let errorMessage = "Please enter a valid todo.";
function addTodo() {
  if (newTodo.value) {
    // Check if newTodo.value is not null, undefined, or an empty string
    if (isUpdate) {
      todos.value.push({ id: temID, text: newTodo.value });
      newTodo.value = "";
      isUpdate = false;
    } else {
      todos.value.push({ id: id++, text: newTodo.value });
      newTodo.value = "";
    }
  } else {
    console.log("Please enter a valid todo.");
    errorMessage = "Please enter a valid todo.";
    alert(errorMessage)
  }
}

// Remove todo function
function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo);
}

// Update todo function
function updateTodoText(todo, newText) {
  const updatedTodo = { id: temID, text: newText }; // Create a new todo object
  todos.value = todos.value.filter((t) => t !== todo);

  ///add text
  console.log(todo.id);
  newTodo.value = newText;
  temID = todo.id;
  isUpdate = true;
}
</script>

