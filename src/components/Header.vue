<template>
  <nav>
    <v-app-bar flat>
      <v-toolbar-title>TaskTrack</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-icon
        @click="$emit('toggle-form')"
        :color="showForm ? 'red' : '#73CB73'"
      >mdi-plus</v-icon>
    </v-app-bar>
  </nav>
</template>

<script>
export default {
  name: 'Header',
  props: {
    showForm: Boolean,
    color: String
  }
}
</script>
