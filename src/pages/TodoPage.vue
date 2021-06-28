<template>
  <Counter :initCount="0" :addBy="1" />
  <!-- <Counter :initCount="10" :addBy="2" />
  <Counter :initCount="20" :addBy="3" /> -->
  <hr />
  <Todo />
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import Todo from '@/components/Todo.vue'
import Counter from '@/components/Counter.vue'

export default defineComponent({
  components: {
    Todo,
    Counter,
  },
})
</script>
