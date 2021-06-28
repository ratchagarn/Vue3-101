<template>
  <h3>Todo App</h3>
  <div>
    <input
      type="text"
      class="form-control"
      placeholder="อยากทำอะไรวันนี้?"
      @keyup.enter="handleOnAddToto"
    />
  </div>

  <hr />

  {{ loading ? 'Loading...' : '' }}

  <TodoItem
    v-for="todo in todoList"
    :key="todo.id"
    :todo="todo"
    @on-completed="handleOncompleted(todo.id)"
    @on-delete="handleOnDelete(todo.id)"
  />
</template>

<script lang="ts">
import { defineComponent, ref, toRaw } from 'vue'
import TodoItem from '@/components/TodoItem.vue'

interface Todo {
  id: number
  label: string
  completed: boolean
}

export default defineComponent({
  components: {
    TodoItem,
  },
  setup() {
    const loading = ref<boolean>(true)
    const todoList = ref<Todo[]>([])

    setTimeout(() => {
      const initTodoList = window.localStorage.getItem('toto-list')
        ? JSON.parse(window.localStorage.getItem('toto-list') as string)
        : []

      todoList.value = initTodoList
      loading.value = false
    }, 1500)

    const syncTodoListToLocalStorage = () => {
      window.localStorage.setItem(
        'toto-list',
        JSON.stringify(toRaw(todoList.value))
      )
    }

    const handleOncompleted = (id: number) => {
      todoList.value = todoList.value.map((todo) => {
        if (todo.id === id) {
          todo.completed = !todo.completed
        }

        return todo
      })

      syncTodoListToLocalStorage()
    }

    const handleOnAddToto = (event: KeyboardEvent) => {
      const input = event.target as HTMLInputElement

      todoList.value.push({
        id: new Date().getTime(),
        label: input.value,
        completed: false,
      })

      input.value = ''

      syncTodoListToLocalStorage()
    }

    const handleOnDelete = (id: number) => {
      todoList.value = todoList.value.filter((todo) => todo.id !== id)

      syncTodoListToLocalStorage()
    }

    return {
      todoList,
      handleOncompleted,
      handleOnAddToto,
      handleOnDelete,
      loading,
    }
  },
})
</script>
