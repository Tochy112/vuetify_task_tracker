<template>
  <nav>
    <v-app-bar flat>
      <v-toolbar-title>TaskTrack</v-toolbar-title>
      <v-spacer></v-spacer>
      <Btn
        @btn-click="$emit('toggle-form')"
        :text="showForm ? 'close' : 'Add'"
        :color="showForm ? 'red' : '#73CB73'"
      />
    </v-app-bar>
  </nav>
</template>

<script>
import Btn from '@/components/Button.vue'
export default {
  name: 'Header',
  props: {
    showForm: Boolean
  },
  components: {
    Btn
  }
}
</script>
