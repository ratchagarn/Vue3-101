<template>
  <button class="btn btn-primary" @click="handleOnClick">Click Me!</button>
  <h1>{{ count }}</h1>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'

export default defineComponent({
  props: {
    initCount: Number,
    addBy: Number,
  },
  setup(props) {
    const count = ref<number>(props.initCount || 0)

    const handleOnClick = () => {
      count.value += props.addBy ? props.addBy : 1
    }

    return {
      count,
      handleOnClick,
    }
  },
})
</script>
