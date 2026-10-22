<script setup>
import { ref } from 'vue';

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

const mostrarCompletadas = () => { }



const toggleEstat = (task) => {
  if (task.estat === 'pendent') {
    task.estat = 'completat';
  } else {
    task.estat = 'pendent';
  }
}

</script>
<template>
  <section class="">
    <h1>Gestor de Tasques</h1>
    <label>Posa la tasca</label>
    <br>
    <input v-model="taskName" type="text" placeholder="Posa el nom de la tasca" />
    <button v-on:click="createTask">Afegir</button>
    <br><br>
    <input type="checkbox" />
    <label for="checkbox">Mostrar només pendents</label>
    <div class="tasks">
      <div v-for="task in tasks" :key="task.id">
        <article class="view-tasks">
          <p :class="{ completed: task.estat === 'completat' }">{{ task.nom }}</p>
          <button v-if="task.estat === 'pendent'" v-on:click="toggleEstat(task)">Completar</button>
          <button v-else-if="task.estat === 'completat'"
            v-on:click="toggleEstat(task)">Desmarcar</button>
          <button v-on:click="deleteTask(task)">🗑️</button>
        </article>
      </div>
    </div>
  </section>

  <section class="account">
    <p>Total: {{ totalTasks }} | Pendets: {{ pendentTasks }}</p>
  </section>
</template>



<style scoped>
.view-tasks {
  display: flex;
  margin: 0;
  padding: 0;
}

.completed {
  text-decoration: line-through;
  opacity: 0.5;
}
</style>