<template>
    <div>
        <ul class="todo-list">
            <TodoItem
              v-for="todo in todos"
              :key="todo.id"
              :todo="todo"
              @toggle-todo="toggleTodo"
              @remove-todo="removeTodo"
            />
        </ul>
    </div>
</template>
<script lang="ts">
import { defineComponent, PropType } from "vue"
import TodoItem from "./TodoItem.vue";
import { Todo } from "@/types/Todo";

export default defineComponent({
  components: { TodoItem },
  props: {
    todos: {
        type: Array as PropType<Todo[]>
    }
  },
  methods: {
    toggleTodo(id:number) {
        this.$emit('toggleTodo', id)
    },
    removeTodo(id:number) {
        this.$emit('removeTodo', id)
    }
  }
})
</script>