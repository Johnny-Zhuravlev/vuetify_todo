<template>
  <div class="home">
    <v-text-field
      v-model="newTaskTitle"
      @click:append="addTask"
      @keyup.enter="addTask"
      outlined
      hide-details
      clearable
      label="Add new task"
      append-icon="mdi-plus-circle-outline"
      class="pa-3"
    ></v-text-field>

    <v-list subheader two-line flat>
      <div v-for="task of tasks" :key="task.id">
        <v-list-item
          @click="doneTask(task.id)"
          :class="{ 'light-blue lighten-4': task.done }"
        >
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox :input-value="task.done" color="primary"></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title
                :class="{ 'text-decoration-line-through': task.done }"
                >{{ task.title }}</v-list-item-title
              >
            </v-list-item-content>

            <v-list-item-action>
              <v-btn @click.stop="deleteTask(task.id)" icon>
                <v-icon color="red">mdi-trash-can-outline</v-icon>
              </v-btn>
            </v-list-item-action>
          </template>
        </v-list-item>
        <v-divider></v-divider>
      </div>
    </v-list>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: "Home",
  data() {
    return {
      newTaskTitle: '',
      tasks: [
        // { id: 1, title: "Brush the teeth", done: false },
        // { id: 2, title: "Make a breakfast", done: false },
        // { id: 3, title: "Help my sister with her dog", done: false },
        // { id: 4, title: "Do workout", done: false },
      ],
    };
  },
  methods: {
    addTask() {
      let newTask = {
        id: Date.now(),
        title: this.newTaskTitle,
        done: false,
      }
      this.tasks.push(newTask);
      this.newTaskTitle = '';
    },
    doneTask(id) {
      let task = this.tasks.filter((task) => task.id === id)[0];
      task.done = !task.done;
    },
    deleteTask(id) {
      this.tasks = this.tasks.filter((task) => task.id !== id);
    },
  },
};
</script>

<style lang="scss">
  .v-app-bar-title__placeholder, .v-app-bar-title__content {
    overflow: visible;
  }
</style>
