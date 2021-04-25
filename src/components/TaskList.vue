<template>
  <div class="task-list">
      <div class="input-group mb-2 mt-5">
          <div class="input-group-prepend">
              <div class="input-group-text">New task :</div>
          </div>
          <input v-model="todoInput" placeholder="task name" class="form-control border border-dark">
          <div class="input-group-append">
              <div class="btn-group ml-1" role="group" aria-label="Basic example">
                  <button v-on:click="addTask(newtask)" class="btn btn-outline-secondary">Add</button>
                  <button v-on:click="removeAllTasks()" class="btn btn-outline-secondary">Remove All</button>
                  <button v-on:click="removeDoneTasks()" class="btn btn-outline-secondary">Remove done tasks</button>
                  <select v-model="selectedFilter" v-on:change="updateListView()" class="form-select btn btn-outline-secondary" aria-label="Default select example">
                      <option selected value="0">All</option>
                      <option value="1">Done</option>
                      <option value="2">To do</option>
                  </select>
              </div>
          </div>
      </div>

      <ul class="list-group list-group-flush border">
          <li v-for="(todo, index) in tasksListView" :key="index" class="list-group-item" :class="{'list-group-item-line-through list-group-item-danger': todo.checked}" >
              <div class="input-group">
                  <div class="input-group-prepend">
                      <div class="input-group-text">
                          <input type="checkbox" v-model="todo.checked" @click="todo.toggleChecked(),updateTasksStats()">
                      </div>
                  </div>
                  <input class="form-control w-50 float-center" v-bind:value="todo.todo" v-on:change="updateTaskName($event,todo)">
                  <div class="input-group-append">
                      <button type="button" class="btn btn-outline-secondary" aria-label="Close" @click.stop="deleteTask(todo)">x</button>
                  </div>
              </div>
          </li>
          <li v-if="nbtasks > 0" class="list-group-item list-group-item-secondary border border-dark">You have {{nbtasks}} tasks, {{nbTasksDone}} done and {{nbTasksToDo}} to do.</li>
          <li v-else class="list-group-item list-group-item-secondary border border-dark">You have no tasks.</li>
      </ul>
  </div>
</template>
<script lang="ts">
  import Vue from 'vue';
  import Component from 'vue-class-component';

  class Todo {
      todo: string;
      checked: boolean;

      constructor(todo: string) {
          this.todo=todo;
          this.checked=false;
      }

      toggleChecked(){
          this.checked = !this.checked;
      }
  }

  @Component({})
  export default class TaskListComponent extends Vue {
      todoInput: string | undefined;
      tasksList: Todo[] = [];
      tasksListView: Todo[] = [];
      nbtasks = this.tasksList.length;
      nbTasksDone = 0;
      nbTasksToDo = 0;
      selectedFilter = '0';

      addTask() {
          console.log("Add new task " + this.todoInput)
          if (this.todoInput != undefined && this.todoInput != "") {
              this.tasksList.push(new Todo(this.todoInput))
              this.updateListView();
          }
      }

      deleteTask(todo: Todo) {
          console.log("Remove " + todo)
          this.tasksList = this.tasksList.filter((todoItem) => {
              return todoItem !== todo;
          })
          this.updateListView();
      }

      removeAllTasks() {
          console.log("Remove all tasks")
          this.tasksList = [];
          this.updateListView();
      }

      updateTasksStats() {
          console.log("Refresh task stats")
          this.nbTasksDone = 0;
          this.nbTasksToDo = 0;
          for (const entry of this.tasksList) {
              if (entry.checked) {
                  this.nbTasksDone++;
              } else {
                  this.nbTasksToDo++;
              }
          }
          this.nbtasks = this.tasksList.length;
      }

      updateListView() {
          console.log("Update list view")
          if(this.selectedFilter=='1'){
              this.tasksListView = this.tasksList.filter(todo => todo.checked);
              console.log(this.tasksListView.length);
          }
          else if(this.selectedFilter=='2'){
              this.tasksListView = this.tasksList.filter(todo => !todo.checked);
              console.log(this.tasksListView.length);
          }
          else{
              this.tasksListView = this.tasksList;
              console.log(this.tasksListView.length);
          }
          this.updateTasksStats();
      }

      removeDoneTasks(){
          console.log("Remove done tasks")
          this.tasksList = this.tasksList.filter(todo => !todo.checked);
          this.updateListView();
      }

      updateTaskName(e: Event, todo: Todo){
          const target = e.target as HTMLTextAreaElement
          todo.todo=target.value;
          console.log(target.value);
          this.updateListView();
      }


  }


</script>

