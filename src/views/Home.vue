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
const api = 'https://mousy-brick-chimpanzee.glitch.me'
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
    async addTask (task) { // add a task to the api using post method
      const res = await fetch(`${api}/tasks`, {
        method: 'POST',
        headers: {
          'Content-type': 'application/json'
        },
        body: JSON.stringify(task)
      })
      const data = await res.json()
      this.tasks = [...this.tasks, data]
    },
    async toggleTask (id) { // update a task in the api using put method
      const taskToToggle = await this.fetchTask(id)
      const updTask = { ...taskToToggle, status: !taskToToggle.status }

      const res = await fetch(`${api}/tasks/${id}`, {
        method: 'PUT',
        headers: {
          'Content-type': 'application/json'
        },
        body: JSON.stringify(updTask)
      })
      const data = await res.json()
      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, status: data.status } : task
      )
    },
    async deleteTask (id) { // deleting a task from the api using delete method
      if (confirm('Are you sure?')) {
        const res = await fetch(`${api}/tasks/${id}`, {
          method: 'DELETE'
        })

        res.status === 200
          ? (this.tasks = this.tasks.filter((task) => task.id !== id))
          : alert('Error occurred deleting this task')
      }
    }, // fetch all the data from api
    async fetchTasks () {
      const res = await fetch(`${api}/tasks`)
      const data = await res.json()
      return data
    }, // fetch a specific data from api
    async fetchTask (id) {
      const res = await fetch(`${api}/tasks/${id}`)
      const data = await res.json()
      return data
    }
  },
  data () {
    return {
      tasks: [],
      showForm: true
    }
  },
  async created () {
    this.tasks = await this.fetchTasks()
  }
}
</script>
