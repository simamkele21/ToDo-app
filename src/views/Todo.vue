<template>
<div class="home">
            <v-text-field
            v-model="newTaskTitle"
            @click:append="addTask"
            @keyup.enter="addTask"
            class="pa-3"
            outlined
            label="What you working on?"
            append-icon="mdi-plus"
            hide-details
            clearable
          ></v-text-field>
                <v-divider class="mt-3"></v-divider>
  
      <v-layout
        my-1
        align-center
      >
        <strong class="mx-3 info--text text--darken-3">
          Remaining: {{ remainingTasks }}
        </strong>
  
        <v-divider vertical></v-divider>
  
        <strong class="mx-3 black--text">
          Completed: {{ completedTasks }}
        </strong>
  
        <v-spacer></v-spacer>
  
        <v-progress-circular
          :value="progress"
          class="mr-2"
        ></v-progress-circular>
      </v-layout>

            <v-divider class="mb-3"></v-divider>

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
export default {
  name: 'Home',
    data() {
      return {
        STORAGE_KEY: 'vue-todo-app-storage',
        newTaskTitle: "",
        tasks: [],
        newTask: ""
      }
    },
    created() {
      this.tasks = JSON.parse(localStorage.getItem(this.STORAGE_KEY) || '[]')
      console.log(this.tasks)
    },
    computed: {
    completedTasks() {
      return this.tasks.filter(task => task.done).length;
    },
    progress() {
      return this.completedTasks / this.tasks.length * 100;
    },
    remainingTasks() {
      return this.tasks.length - this.completedTasks;
    } },
    
    methods: {

      addTask() {
        let newTask = {
          id: Date.now(),
          title: this.newTaskTitle,
          done: false
        }
        this.tasks.push(newTask)
        this.newTaskTitle = ''  
        localStorage.setItem(this.STORAGE_KEY, JSON.stringify(this.tasks));
      },
      doneTask(id) {
        let task = this.tasks.filter( task => task.id === id) [0]
        task.done = !task.done
        localStorage.setItem(this.STORAGE_KEY, JSON.stringify(this.tasks));
      },
      deleteTask(id) {
        this.tasks = this.tasks.filter(task => task.id !== id)
        localStorage.setItem(this.STORAGE_KEY, JSON.stringify(this.tasks));
      }
    }
  }
  
</script>
<style scoped>
.v-list{
background-color: rgb(194, 193, 193);
}
</style>