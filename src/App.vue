<template>
  <div id="app">
    <HeaderApp/>

    <FiltersApp />

    <main class="app-main">
      <TodoList/>

      <AddTodo/>
    </main>
<FooterApp />
  </div>
</template>

<script lang="ts">
import HeaderApp from './components/HeaderApp.vue';
import FiltersApp from './components/FiltersApp.vue';
import TodoList from './components/TodoList.vue';
import AddTodo from './components/AddTodo.vue';
import FooterApp from './components/FooterApp.vue';

export default {
  name: 'App',
  components: {
    HeaderApp,
    FiltersApp,
    TodoList,
    AddTodo,
    FooterApp
  }
};
</script>


