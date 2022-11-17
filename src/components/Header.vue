<template>
  <nav>
    <v-app-bar flat>
      <v-toolbar-title> Track<span>eet</span> </v-toolbar-title>
      <v-spacer></v-spacer>
          <v-row justify="center">
            <v-btn color="success" small class="mt-2" @click="overlay = !overlay">
              Tip
            </v-btn>

            <v-overlay :value="overlay" :opacity="opacity" height="200px">
              Double click on a task to update its status.
              <span class="red--text">Red</span>= Undone. <span style="color:#73cb73;">Green</span>= Done
              <v-btn color="success" class="mx-auto" small @click="overlay = false">
                close
              </v-btn>
            </v-overlay>
          </v-row>
      <v-spacer></v-spacer>
      <v-icon
        @click="$emit('toggle-form')"
        :color="showForm ? 'red' : '#73CB73'"
        >mdi-plus</v-icon
      >
    </v-app-bar>
  </nav>
</template>

<script>
export default {
  name: 'Header',
  props: {
    showForm: Boolean,
    color: String
  },
  data () {
    return {
      overlay: false,
      opacity: 0.9
    }
  }
}
</script>

<style scoped>
span {
  color: #73cb73;
  font-family: cursive;
}
</style>
