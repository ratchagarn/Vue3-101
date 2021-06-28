<template>
  <div class="todo-list">
    <div>
      <input
        type="checkbox"
        :checked="todo.completed"
        @click="context.emit('on-completed')"
      />
    </div>
    <div :class="{ completed: todo.completed }">{{ todo.label }}</div>
    <div>
      <button class="btn btn-danger" @click="context.emit('on-delete')">
        ลบ
      </button>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue'

interface Todo {
  id: number
  label: string
  completed: boolean
}

export default defineComponent({
  emits: ['on-completed', 'on-delete'],
  props: {
    todo: Array as PropType<Todo[]>,
  },
  setup(_, context) {
    return {
      context,
    }
  },
})
</script>

<style scoped>
.todo-list {
  display: flex;
  margin-bottom: 16px;
}

.todo-list > div {
  padding: 8px;
}

.completed {
  text-decoration: line-through;
  opacity: 0.4;
}
</style>
