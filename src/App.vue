<script setup>
import { ref, reactive } from 'vue';

    const tasks = reactive([
      { name: 'Task 1', time: 60 },
      { name: 'Task 2', time: 75 },
    ]);

    const showAddTaskModal = ref(false);
    const newTaskName = ref('');
    const newTaskTime = ref(0);

    const removeTask = (index) => {
      tasks.splice(index, 1);
    };

    const addTask = () => {
      if (newTaskName.value && newTaskTime.value) {
        tasks.push({ name: newTaskName.value, time: newTaskTime.value });
        newTaskName.value = '';
        newTaskTime.value = 0;
        showAddTaskModal.value = false;
      }
    };

</script>


<template>
  <div class="container">
    <h2>Tasks List</h2>

    <table>
      <thead>
        <tr>
          <th>Task Name</th>
          <th>Time (minutes)</th>
          <th>Action</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
          <td>{{ task.name }}</td>
          <td>{{ task.time }}</td>
          <td>
            <button class="delete" @click="removeTask(index)">Remove</button>
          </td>
        </tr>
      </tbody>
    </table>

    <button class="add_task" @click="showAddTaskModal = true">Add Task</button>

    <div v-if="showAddTaskModal" class="modal">
      <!-- <h3>Add Task</h3> -->
      <form @submit.prevent="addTask">
        <label for="taskName">Task Name:</label>
        <input type="text" id="taskName" v-model="newTaskName">
        <label for="taskTime">Time (minutes):</label>
        <input type="number" id="taskTime" v-model="newTaskTime">
        <button class="add" type="submit">Add</button>
        <button class="cancel" @click="showAddTaskModal = false">Cancel</button>
      </form>
    </div>
  </div>
</template>

<style scoped>
  table {
    width: 100%;
    border-collapse: collapse;
    margin-top: 10px;
  }

  th, td {
    border: 1px solid #ddd;
    padding: 8px;
    text-align: left;
  }

  th {
    background-color: #f2f2f2;
  }

  .add_task {
    background-color: greenyellow;
    margin-top: 30px;
  }

  form {
    margin-top: 20px;
    display: flex;
    flex-direction: column;
  }

  input {
    line-height: 1.5rem!important;
    margin-top: 10px;
  }

  .delete {
    background-color: red;
    padding: 0.2rem 0.6rem;
    font-weight: normal;
  }

  .add {
    background-color: greenyellow;
    margin-top: 10px;
    padding: 0.4rem .8rem;
    font-weight: normal;
  }

  .cancel {
    background-color: crimson;
    margin-top: 10px;
    padding: 0.4rem .8rem;
    font-weight: normal;
  }
</style>

