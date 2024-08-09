<template>
  <main>
    <!-- heading -->
     <header>
      <img src="./assets/pinia-logo.svg" alt="pinia logo">
      <h1>{{ taskStore.name }}</h1>
    </header>

    <!-- task list -->
     <div class="task-list">
      <div v-for="task in taskStore.tasks" :key="task">
        <TaskDetails :task="task"/>
      </div>
     </div>
  </main>
</template>

<script>
import { useTaskStore } from './stores/TaskStore';
import TaskDetails from './components/TaskDetails.vue';

export default {
  components: { TaskDetails },
  setup () {
    const taskStore = useTaskStore();

    return {taskStore};
  }
};
</script>
