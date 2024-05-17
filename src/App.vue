<template>
  <main>
    <header>
      <img src="./assets/pinia-logo.png" alt="pinia logo">
      <h1>Pinia Tasks</h1>
    </header>

    <!-- new task form -->
    <div class="new-task-form">
      <TaskForm/>
    </div>

    <!-- filter -->
    <nav class="filter">
      <button @click="filter = 'all'">All tasks</button>
      <button @click="filter = 'favs'">Fav tasks</button>
    </nav>

    <!-- loading -->
    <div class="loading" v-if="taskStore.loading">Loading tasks...</div>

    <div class="task-list" v-if="filter === 'all'">
      <p>You have {{ taskStore.totalCount }} tasks</p>
      <div v-for="task in taskStore.tasks" :key="task.id">
        <TaskDetails :task="task"/>
      </div>
    </div>

    <div class="task-list" v-if="filter === 'favs'">
      <p>You have {{ taskStore.favCount}} favs left to do</p>
      <div v-for="task in taskStore.favs" :key="task.id">
        <TaskDetails :task="task"/>
      </div>
    </div>
  </main>
</template>

<script>
import {useTaskStore} from './stores/TaskStore'
import TaskDetails from './components/TaskDetails.vue'
import TaskForm from './components/TaskForm.vue';
import { ref } from 'vue'

export default {
  components: {TaskDetails, TaskForm},
  setup(){
    const taskStore = useTaskStore()

    taskStore.getTasks()

    const filter = ref('all')
    return {taskStore, filter}
  }
}
</script>
