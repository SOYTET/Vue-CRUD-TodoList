<template>
  <div> <!-- Adding margin x-axis (horizontal) and y-axis (vertical) -->
    <header-page class="mb-10"></header-page> <!-- Adding margin bottom -->
    <TodoList class="mt-10"></TodoList> <!-- Adding margin top -->
  </div>
</template>


<script>
import TodoList from './components/CRUD_TodoList.vue';
import HeaderPage from './components/HeaderPage.vue';


export default {
  name: "App",
  components: {
    TodoList,
    HeaderPage,
  }
};
</script>
