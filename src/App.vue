<template>
  <div id="app">
    <HeaderApp />

    <FiltersApp />

    <main class="app-main">
      <TodoList :todos="todos"
        @toggle-todo="toggleTodo"
        @remove-todo="removeTodo" />

      <AddTodo @add-todo="addTodo" />
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
import { Todo } from './types/Todo';
import { defineComponent } from 'vue';
interface State {
  todos: Todo[]
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
        ]
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
    }
  }
})
</script>


