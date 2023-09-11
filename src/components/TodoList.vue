<template>
    <div>
        <ul class="todo-list">
            <TodoItem v-for="todo in todos" :key="todo.id" :todo="todo" @toggle-todo="toggleTodo" />
        </ul>
    </div>
</template>
<script lang="ts">
import { defineComponent } from "vue"
import TodoItem from "./TodoItem.vue";
import { Todo } from "@/types/Todo";

interface State {
  todos: Todo[]
}

export default defineComponent({
  components: { TodoItem },
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
    toggleTodo(id:number) {
        console.log(id);
        const targetTodo = this.todos.find((todo: Todo) => todo.id === id);
        if(targetTodo) {
            targetTodo.completed = !targetTodo.completed;
        }
    }
  }
})
</script>