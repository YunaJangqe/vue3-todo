<template>
  <TodoHeader :appTitle="title"></TodoHeader>
  <TodoInput @add="addTodoItem"></TodoInput>
  <TodoList :items="todoItems" @remove="removeTodoItem"></TodoList>
</template>

<script>
  import TodoHeader from '@/components/TodoHeader.vue';
  import TodoInput from './components/TodoInput.vue';
  import TodoList from './components/TodoList.vue';
  import { useTodo } from './composable/useTodo';

  export default {
    components: {
      TodoHeader,
      TodoInput,
      TodoList
    },
    data() {
      return {
        title: '할일 앱'
      }
    },
    setup() {
      const { todoItems, addTodoItem, removeTodoItem, fetchTodos } = useTodo();

      // 라이플 사이클 API
      onBeforeMount(() => {
        todoItems.value = fetchTodos();
    })

      return { todoItems, addTodoItem, removeTodoItem }
    }
  }
</script>

<style scoped>

</style>