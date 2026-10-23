<script setup>
import { ref, computed } from 'vue';

class Task {
  id;
  nom;
  estat;
  constructor(id, nom, estat) {
    this.id = id;
    this.nom = nom;
    this.estat = estat;
  }
}

const tasks = ref([]);

const taskName = ref('');

const createTask = () => {
  const name = taskName.value.trim();
  if (!name) return;

  const newTask = new Task(tasks.value.length + 1, name, "pendent");
  tasks.value.push(newTask);
  taskName.value = '';
}

const deleteTask = (taskToDelete) => {
  tasks.value = tasks.value.filter(task => task.id !== taskToDelete.id);
}


const totalTasks = computed(() => tasks.value.length);

const pendentTasks = computed(() => {
  return tasks.value.filter(task => task.estat === 'pendent').length;
});


const viewCompleted = ref()

let completedTasks = []

const completedTaksOnly = computed(() => {
  completedTasks = tasks.value.filter(task => task.estat === 'pendent')
  return completedTasks
});



const toggleEstat = (task) => {
  if (task.estat === 'pendent') {
    task.estat = 'completat';
  } else {
    task.estat = 'pendent';
  }
}

</script>
<template>
  <main class="app">
    <section class="card">
      <h1>Gestor de Tasques</h1>

      <label class="label">Posa la tasca</label>
      <div class="input-row">
        <input v-model="taskName" type="text" placeholder="Posa el nom de la tasca" />
        <button class="add-btn" v-on:click="createTask">Afegir</button>
      </div>

      <label class="check-row">
        <input v-model="viewCompleted" type="checkbox" />
        <span>Mostrar només pendents</span>
      </label>

      <div class="tasks" v-if="!viewCompleted">
        <div v-for="task in tasks" :key="task.id" class="task-item">
          <article class="view-tasks">
            <p :class="{ completed: task.estat === 'completat' }">{{ task.nom }}</p>
            <div class="task-actions">
              <button v-if="task.estat === 'pendent'" v-on:click="toggleEstat(task)">Completar</button>
              <button v-else-if="task.estat === 'completat'" v-on:click="toggleEstat(task)">Desmarcar</button>
              <button class="delete-btn" v-on:click="deleteTask(task)">🗑️</button>
            </div>
          </article>
        </div>
      </div>

      <div class="tasks" v-else>
        <div v-for="task in completedTaksOnly" :key="task.id" class="task-item">
          <article class="view-tasks">
            <p :class="{ completed: task.estat === 'completat' }">{{ task.nom }}</p>
            <div class="task-actions">
              <button v-if="task.estat === 'pendent'" v-on:click="toggleEstat(task)">Completar</button>
              <button v-else-if="task.estat === 'completat'" v-on:click="toggleEstat(task)">Desmarcar</button>
              <button class="delete-btn" v-on:click="deleteTask(task)">🗑️</button>
            </div>
          </article>
        </div>
      </div>
    </section>

    <section class="account">
      <p>Total: {{ totalTasks }} | Pendets: {{ pendentTasks }}</p>
    </section>
  </main>
</template>

<style scoped>
:global(body) {
  margin: 0;
  font-family: Arial, sans-serif;
  background: #f3f4f6;
}

* {
  box-sizing: border-box;
}

.app {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
  padding: 24px;
}

.card {
  width: min(100%, 500px);
  background: #ffffff;
  border-radius: 16px;
  box-shadow: 0 8px 22px rgba(0, 0, 0, 0.08);
  padding: 24px;
}

h1 {
  margin: 0 0 20px;
  text-align: center;
  color: #1f2937;
}

.label {
  display: block;
  margin-bottom: 8px;
  color: #374151;
  font-weight: bold;
}

.input-row {
  display: flex;
  gap: 10px;
  margin-bottom: 16px;
}

input[type='text'] {
  flex: 1;
  border: 1px solid #d1d5db;
  border-radius: 10px;
  padding: 10px 12px;
}

.add-btn,
.view-tasks button {
  border: none;
  border-radius: 10px;
  padding: 10px 12px;
  cursor: pointer;
}

.add-btn {
  background: #4f46e5;
  color: white;
  font-weight: bold;
}

.check-row {
  display: flex;
  align-items: center;
  gap: 8px;
  margin-bottom: 18px;
  color: #4b5563;
}

.tasks {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.task-item {
  background: #f9fafb;
  border: 1px solid #e5e7eb;
  border-radius: 12px;
  padding: 8px 12px;
}

.view-tasks {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 10px;
}

.view-tasks p {
  margin: 0;
  flex: 1;
  color: #111827;
}

.task-actions {
  display: flex;
  align-items: center;
  gap: 8px;
}

.view-tasks button {
  background: #e0f2fe;
  color: #0f172a;
}

.delete-btn {
  background: #fee2e2;
}

.completed {
  text-decoration: line-through;
  opacity: 0.6;
}

.account {
  margin-top: 16px;
  text-align: center;
  color: #374151;
}

.account p {
  margin: 0;
}
</style>