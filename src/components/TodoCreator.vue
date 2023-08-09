<script setup lang="ts">
import { ref, type Ref } from 'vue';

const emit = defineEmits(["create-todo"])

// ref method
const todo: Ref<string> = ref("")
const error: Ref<string|null> = ref(null)
// ref method end

// reactive method
// const todoState = reactive({
//     todo: ""
// })
// console.log(todoState.todo)
// reactive method end

const createTodo = (): void => {
    error.value = null

    if (!todo.value) error.value = "Please enter a ToDo."
    
    if (!error.value) {
        emit("create-todo", todo.value)
        todo.value = ""
    }
}
</script>

<template>
    <div class="input-wrap" :class="{ 'input-err': error }">
        <input type="text" placeholder="New todo" v-model="todo" />
        <button @click="createTodo()">Create</button>
    </div>
    <div v-show="error" class="error">{{ error }}</div>
</template>

<style scoped lang="scss">
.input-wrap {
    display: flex;
    transition: 250ms ease;
    border: 2px solid #41b080;

    &:focus-within {
        box-shadow: 0 -4px 6px -1px rgb(0 0 0 / 0.1),
        0 -2px 4px -2px rgb(0 0 0 / 0.1);
    }

    &.input-err {
        border-color: red;
    }

    input {
        width: 100%;
        padding: 8px 6px;
        border: none;

        &:focus {
        outline: none;
        }
    }

    button {
        padding: 8px 16px;
        border: none;
    }
}

.error {
    color: red;
    margin: .5rem 0;
    text-align: center;
}
</style>