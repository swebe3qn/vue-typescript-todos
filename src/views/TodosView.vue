<script setup lang="ts">
import { ref, watch, type Ref, computed } from "vue";
import { uid } from "uid"
import TodoCreator from "../components/TodoCreator.vue";
import TodoItem from "../components/TodoItem.vue";
import { type ToDoInterface } from "../interfaces/ToDo";

const todoList: Ref<ToDoInterface[]> = ref([])

watch(todoList, () => setTodoListLocalStorage(), {
  deep: true
})

const todosCompleted = computed(() => {
  return todoList.value.every(todo => todo.isCompleted)
})

const setTodoListLocalStorage = () => {
  localStorage.setItem("todoList", JSON.stringify(todoList.value))
}

const fetchTodoList = () => {
  const data = localStorage.getItem("todoList")

  if (data) todoList.value = JSON.parse(data)
}

fetchTodoList()

const createTodo = (val: string): void => {
  todoList.value.push({
    id: uid(),
    todo: val,
    isCompleted: false,
    isEditing: false
  })
}

const toggleComplete = (index: number): void => {
  if (typeof todoList.value[index] !== 'undefined') todoList.value[index].isCompleted = !todoList.value[index].isCompleted
}

const toggleEditTodo = (index: number): void => {
  if (typeof todoList.value[index] !== 'undefined') todoList.value[index].isEditing = !todoList.value[index].isEditing
}

const deleteTodo = (index: number): void => {
  if (typeof todoList.value[index] !== 'undefined') todoList.value.splice(index, 1)
}

const updateTodo = (index: number, val: string): void => {
  if (typeof todoList.value[index] !== 'undefined') todoList.value[index].todo = val
}
</script>

<template>
  <main class="container">
    <h1>Create Todo</h1>
    <TodoCreator @create-todo="createTodo" />
    <ul v-if="todoList.length >= 1">
      <TodoItem 
        v-for="(todo, index) in todoList" 
        :key="todo.id" 
        :index="index"
        :todo="todo" 
        @toggle-complete="toggleComplete" 
        @edit-todo="toggleEditTodo" 
        @delete-todo="deleteTodo"
        @update-todo="updateTodo"
      />
    </ul>
    <p v-else class="msg">
      You don't have any todos in your list. Add one!
    </p>
    <p v-if="todosCompleted && todoList.length > 0" class="msg">All todos completed. Great job!</p>
  </main>
</template>

<style scoped lang="scss">
main {
  display: flex;
  flex-direction: column;
  max-width: 500px;
  width: 100%;
  margin: 0 auto;
  padding: 40px 16px;

  h1 {
    margin-bottom: 16px;
    text-align: center;
  }

  .msg {
    margin: .5rem auto;
    text-align: center;
  }
}
</style>
../interfaces/ToDo