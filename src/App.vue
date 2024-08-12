<template>
  <main>
    <!-- heading -->
    <header>
      <img src="./assets/pinia-logo.svg" alt="pinia logo" />
      <h1>{{ taskStore.name }}</h1>
    </header>

    <!-- new task form -->
    <div class="new-task-form">
      <TaskForm />
    </div>

    
    <!-- filter button  -->
    <nav class="filter">
      <button @click="filter = 'all'">All tasks</button>
      <button @click="filter = 'favs'">Fav tasks</button>
    </nav>
    
    <!-- loading task  -->
    <div class="loading" v-if="loading">
      Loading tasks...
    </div>

    <!-- task list -->
    <div class="task-list" v-if="filter === 'all'">
      <p>Your have {{ totalCount }} tasks left to do</p>
      <div v-for="task in tasks" :key="task">
        <TaskDetails :task="task" />
      </div>
    </div>

    <!-- task favs -->
    <div class="task-list" v-if="filter === 'favs'">
      <p>Your have {{ favCount }} fav left to do</p>
      <div v-for="task in favs" :key="task">
        <TaskDetails :task="task" />
      </div>
    </div>
  </main>
</template>

<script>
import { useTaskStore } from "./stores/TaskStore";
import TaskDetails from "./components/TaskDetails.vue";
import TaskForm from "./components/TaskForm.vue";
import { ref } from "vue";
import { storeToRefs } from "pinia";

export default {
  components: { TaskDetails, TaskForm },
  setup() {
    const taskStore = useTaskStore();

    const {tasks, loading, totalCount, favCount, favs } = storeToRefs(taskStore)

    taskStore.getTasks();

    const filter = ref("all");

    return { taskStore, filter, tasks, loading, totalCount, favCount, favs };
  },
};
</script>
