<template>
  <div id="app">
    <HeaderApp />

    <FiltersApp :activeFilter="'Active'" @set-filter="setFilter" />

    <main class="app-main">
      <TodoList :todos="filteredTodos"
        @toggle-todo="toggleTodo"
        @remove-todo="removeTodo" />

      <AddTodo @add-todo="addTodo" />
    </main>
    <FooterApp :stats="stats" />
  </div>
</template>

<script lang="ts">
import HeaderApp from './components/HeaderApp.vue';
import FiltersApp from './components/FiltersApp.vue';
import TodoList from './components/TodoList.vue';
import AddTodo from './components/AddTodo.vue';
import FooterApp, { Stats } from './components/FooterApp.vue';
import { Todo } from './types/Todo';
import { defineComponent } from 'vue';
import { Filter } from './types/Filter';
interface State {
  todos: Todo[],
  activeFilter: Filter

}
export default defineComponent({
  components: {
    HeaderApp,
    FiltersApp,
    TodoList,
    AddTodo,
    FooterApp
  },
  data(): State{
    return {
        todos: [
          {id:0, text: 'Learn the basics', completed: true},
          {id:1, text: 'Learn', completed: false},
          {id:2, text: 'Learn the basics of Vue', completed: false}
        ],
        activeFilter: 'All'
    }
  },
  computed: {
    filteredTodos(): Todo[] {
      switch (this.activeFilter){
        case 'Active':
          return this.activeTodos;
        case 'Done':
          return this.doneTodos;
        case 'All':
        default:
          return this.todos
      }
    },
    stats(): Stats {
      return {
        active: this.activeTodos.length,
        done: this.doneTodos.length,
      }
    },
    activeTodos(): Todo[] {
      return this.todos.filter(todo => !todo.completed);
    },
    doneTodos(): Todo[] {
      return this.todos.filter(todo => todo.completed)
    }
  },
  methods: {
    addTodo(todo: Todo) {
      this.todos.push(todo)
    },
    toggleTodo(id:number) {
      const targetTodo = this.todos.find((todo: Todo) => todo.id === id);
      if(targetTodo) {
          targetTodo.completed = !targetTodo.completed;
      }
    },
    removeTodo(id:number) {
      this.todos = this.todos.filter((todo: Todo) => todo.id !==id)
    },
    setFilter(filter: Filter) {
      this.activeFilter = filter;
    }
  }
})
</script>


