<template>
  <v-container>
    <v-card elevation="2" class="mx-auto mt-9" max-width="550">
      <!-- header -->
      <Header @toggle-form="toggleForm"/>
      <!-- add task form -->
      <AddTask @add-task="addTask" v-if="showForm"/>
      <!-- individual task -->
      <Tasks :tasks="tasks" @toggle_task="toggleTask" @delete_task="deleteTask"/>
    </v-card>
  </v-container>
</template>

<script>
import Header from '@/components/Header.vue'
import Tasks from '@/components/Tasks.vue'
import AddTask from '@/components/AddTask.vue'
export default {
  name: 'Home',
  components: {
    Header,
    Tasks,
    AddTask
  },
  methods: {
    toggleForm () {
      this.showForm = !this.showForm
    },
    addTask (task) {
      this.tasks = [...this.tasks, task]
    },
    toggleTask (id) {
      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, status: !task.status } : task
      )
    },
    deleteTask (id) {
      this.tasks = this.tasks.filter((task) => task.id !== id)
    }
  },
  data () {
    return {
      tasks: [],
      showForm: true
    }
  },
  created () {
    this.tasks = [
      // {
      //   id: 1,
      //   text: 'Doctors Appointment',
      //   day: 'March 1st at 2:30pm',
      //   status: true
      // },
      // {
      //   id: 2,
      //   text: 'Meeting at School',
      //   day: 'March 3rd at 1:30pm',
      //   status: true
      // },
      // {
      //   id: 3,
      //   text: 'Food Shopping',
      //   day: 'March 3rd at 10:00am',
      //   status: false
      // }
    ]
  }
}
</script>
