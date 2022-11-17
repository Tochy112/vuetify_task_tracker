<template>
  <v-container>
    <v-card flat>
      <v-form ref="form" lazy-validation>
        <!-- text-field -->
        <v-text-field
          label="Title"
          v-model="title"
          prepend-icon="mdi-pencil"
          :rules="inputRules"
        ></v-text-field>

        <!-- check box -->
        <v-checkbox v-model="status" v-if="displayCheck"></v-checkbox>
        <!-- date picker -->
        <v-dialog
          ref="dialog"
          v-model="modal"
          :return-value.sync="date"
          persistent
          width="290px"
        >
          <template v-slot:activator="{ on, attrs }">
            <v-text-field
              v-model="date"
              label="Pick a date"
              prepend-icon="mdi-calendar"
              readonly
              v-bind="attrs"
              v-on="on"
              :rules="dateRules"
            ></v-text-field>
          </template>
          <v-date-picker v-model="date" scrollable>
            <v-spacer></v-spacer>
            <v-btn text color="primary" @click="modal = false"> Cancel </v-btn>
            <v-btn text color="primary" @click="$refs.dialog.save(date)">
              OK
            </v-btn>
          </v-date-picker>
        </v-dialog>

        <!-- submit button -->
        <v-btn color="success lighten-1" @click="handleSubmit" :loading="loading" width="100%"
          >Add Task</v-btn
        >
      </v-form>
    </v-card>
  </v-container>
</template>

<script>
export default {
  name: 'AddTask',
  data () {
    return {
      dialog: false,
      modal: false,
      title: '',
      date: '',
      loading: false,
      displayCheck: false,
      status: false,
      inputRules: [(v) => !!v || "Field can't be empty"],
      dateRules: [(v) => !!v || 'Choose a date']
    }
  },
  methods: {
    handleSubmit () {
      if (this.$refs.form.validate()) {
        this.loading = true
        const newTask = {
          // id: Math.floor(Math.random() * 100000),
          text: this.title,
          day: this.date,
          status: this.status
        }
        this.$refs.form.reset()

        setTimeout(() => {
          this.loading = false
        }, 1500)
        this.$emit('add-task', newTask)
        this.$emit(this.taskAdded)
      }
    }
  }
}
</script>
