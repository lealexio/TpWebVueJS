<template>
  <div class="task-list">
      <div class="input-group mb-2 mt-5">
          <div class="input-group-prepend">
              <div class="input-group-text">New task :</div>
          </div>
          <input v-model="todoInput" placeholder="task name" class="form-control border border-dark">
          <div class="input-group-append">
              <div class="btn-group ml-1" role="group" aria-label="Basic example">
                  <button v-on:click="addTask()" class="btn btn-outline-secondary">Add</button>
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

      <TaskItem :tasksListView="tasksListView" :updateTasksStats="updateTasksStats" :deleteTask="deleteTask" :updateTaskName="updateTaskName" ></TaskItem>
      <p v-if="nbtasks > 0" class="list-group-item list-group-item-secondary border border-dark">You have {{nbtasks}} tasks, {{nbTasksDone}} done and {{nbTasksToDo}} to do.</p>
      <p v-else class="list-group-item list-group-item-secondary border border-dark">You have no tasks.</p>

  </div>
</template>
<script lang="ts">
  import Vue from 'vue';
  import Component from 'vue-class-component';
  import TaskItem from "@/components/TaskItem.vue";

  //Representation of a Todo element
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

  @Component({
      components: {TaskItem}
  })
  export default class TaskListComponent extends Vue {
      todoInput ="";
      tasksList: Todo[] = [];
      tasksListView: Todo[] = [];
      nbtasks = this.tasksList.length;
      nbTasksDone = 0;
      nbTasksToDo = 0;
      selectedFilter = '0';

      //Adding a task to the list
      addTask() {
          console.log("Add new task " + this.todoInput)
          if (this.todoInput != undefined && this.todoInput != "") {
              this.tasksList.push(new Todo(this.todoInput))
              this.updateListView();
              this.todoInput="";
          }
      }

      //Remove a task of the list
      deleteTask(todo: Todo) {
          console.log("Remove " + todo)
          this.tasksList = this.tasksList.filter((todoItem) => {
              return todoItem !== todo;
          })
          this.updateListView();
      }

      //Remove all tasks
      removeAllTasks() {
          console.log("Remove all tasks")
          this.tasksList = [];
          this.updateListView();
      }

      //Refresh task stats
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

