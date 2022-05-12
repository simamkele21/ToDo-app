<template>
<div class="home">
            <v-text-field
            v-model="newTaskTitle"
            @click:append="addTask"
            @keyup.enter="addTask"
            class="pa-3"
            outlined
            label="Add task"
            append-icon="mdi-plus"
            hide-details
            clearable
          ></v-text-field>
    <v-list
    class="pt-0"
      flat
    >
    <div
        v-for="task in tasks"
        :key="task.id"
        >
        <v-list-item 
        @click="doneTask(task.id)"
        :class="{ 'brown lighten-2' : task.done}"
        >
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox :input-value="task.done"></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title
              :class="{ 'text-decoration-line-through' : task.done }">
                {{ task.title }}
                </v-list-item-title>
            </v-list-item-content>

                  <v-list-item-action>
          <v-btn 
          @click.stop="deleteTask(task.id)"
          icon>
            <v-icon color="grey lighten-1">mdi-delete</v-icon>
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
<<<<<<< HEAD


export default {
    name: 'Home',
=======
  // new Vue({
    //   el:".todoapp",
  //   data() {
    //     return {
      //       tasks: [],
  //       newTask: "",
  //       editedTask: null,
  //       editedTaskText: null,
  //     }
  //   },
  //   created() {
  //     this.tasks = JSON.parse(localStorage.getItem(STORAGE_KEY) || '[]')
  //   },
  //   methods: {
  //     addTask() {
  //       this.tasks.push({
  //         id:3,
  //         taskCompletionToggleButtonState: "",
  //         taskCompletionState:"incomplete",
  //         text: this.newTask
  //       })
  //       this.newTask = "";
        
  //       localStorage.setItem(STORAGE_KEY, JSON.stringify(this.tasks));
  //   }
  // },
  // deleteTask(task) {
  //   this.tasks.splice(this.indexof(task), 1);
  //   localStorage.setItem(STORAGE_KEY, JSON.stringify(this.tasks));
  // },
  // editTask(task) {
    //   this.editedTask = task;
  //   this.editedTaskText = task.text;
  // },
  // updatedTask(task) {
    //   if(!this.editedTask) {
      //     return;
  //   } else if( !task.text) {
  //     this.deleteTask(task);
  //   }

  //   this.editedTodo  = null;
  //   task.text = this.editedTaskText.trim();

  //   localStorage.setItem(STORAGE_KEY, JSON.stringify(this.tasks));
  // },
  // toggleTaskCompletionState(task) {
  //   if (task.taskCompletionStateToggleButtonState === "" ||  task.taskCompletionStateToggleButtonState === false) {
    //     task.taskCompletionStateToggleButtonState == "checked";
  //     task.taskCompletionState = "completed";
  //   }else if (task.taskCompletionStateToggleButtonState = "checked" || 
  //   task.taskCompletionStateToggleButtonState === true) {
  //     task.taskCompletionStateToggleButtonState = "checked";
  //     task.taskCompletionState = "incomplete";
  //   }
  // }
  // })
STORAGE_KEY = 'vue-todo-app-storage';
export default {
  name: 'Home',
>>>>>>> 09f88e60a02c008608f3b69da0dd758bc0032d44
    data() {
      return {
        newTaskTitle: "",
        tasks: [],
        newTask: ""
      }
    },
    created() {
      this.newTask = JSON.parse(localStorage.getItem(STORAGE_KEY) || '[]')
    },
    methods: {

      addTask() {
        let newTask = {
          id: Date.now(),
          title: this.newTaskTitle,
          done: false
        }
        this.tasks.push(newTask)
        this.newTaskTitle = ''  
        localStorage.setItem(STORAGE_KEY, JSON.stringify(this.tasks));
      },
      doneTask(id) {
        let task = this.tasks.filter( task => task.id === id) [0]
        task.done = !task.done
        localStorage.setItem(STORAGE_KEY, JSON.stringify(this.tasks));
      },
      deleteTask(id) {
        this.tasks = this.tasks.filter(task => task.id !== id)
        localStorage.setItem(STORAGE_KEY, JSON.stringify(this.tasks));
      }
    }
  }
  
</script>
