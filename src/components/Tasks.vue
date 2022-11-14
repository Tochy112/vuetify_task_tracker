<template>
  <v-container>
    <div v-for="task in tasks" :key="task.id">
      <Task @toggle_task="$emit('toggle_task', task.id)" @delete_task="$emit('delete_task', task.id)" :task="task" />
    </div>
  </v-container>
</template>

<script>
import Task from '@/components/Task.vue'
export default {
  name: 'Tasks',
  props: {
    tasks: Array
  },
  components: {
    Task
  },
  emit: ['toggle_task']
}
</script>
