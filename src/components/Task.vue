<template>
  <v-container class="task">
    <v-card
      max-height="200"
      @dblclick="$emit('toggle_task', task.id)"
      :class="[task.status ? 'status' : '', 'd-flex default']"
    >
      <div>
        <v-card-title>{{ task.text }}</v-card-title>
        <v-card-text>{{ task.day }}</v-card-text>
      </div>
      <v-spacer></v-spacer>
      <v-card-actions>
        <v-btn @click="$emit('delete_task', task.id)" fab depressed> <v-icon class="">mdi-delete</v-icon> </v-btn>
      </v-card-actions>
    </v-card>
  </v-container>
</template>

<script>
export default {
  name: 'Task',
  props: {
    task: Object
  }
}
</script>

<style>
.default {
  border-left: 5px solid red !important
}
.default.status{
  border-left: 5px solid #73CB73 !important
}
</style>
