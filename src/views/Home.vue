<template>
  <div class="home container">
    <!--
    <p v-if="visible">Maintenant vous me voyez {{message}}</p>
    <button v-on:click="foo()">ok</button>
    <div v-background>Undefined color</div>
    <div v-background="green">Defined color</div>
    -->

    <TaskListComponent/>
  </div>
</template>

<script lang="ts">
  import { Component, Vue } from 'vue-property-decorator';
  import {Background} from '@/directives/Background.directive'
  import TaskListComponent from "@/components/TaskList.vue";
  @Component({
    components: {
      TaskListComponent,
    },
    directives:{
      Background
    }
  })
  export default class Home extends Vue {

    message= 'test';
    visible = true;
    foo(){
      this.visible = !this.visible;
    }
  }
</script>
