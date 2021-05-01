<template>
  <div>
    <h1>Vue to-do list</h1>
    <label>
      Nova tarefa:
      <input
        autofocus
        type="text"
        @keyup.enter="newTask"
      >
    </label>

    <p>Lista de tarefas:</p>

    <ul v-if="!!tasks && tasks.length > 0">
      <li
        v-for="(task, index) of tasks"
        :key="task.description + index"
      >
        <button
          @click="removeTask(task)"
          class="waves-effect waves-light btn-small red"
        >x
          </button>

          <button
            @click="completeTask(task)"
            class="waves-effect waves-light btn-small"
            :disabled="task.isCompleted()"
          >
            ✓
            </button>
            &nbsp;&nbsp;&nbsp;
            <span :class="task.isCompleted() && 'completed'">{{ task.description }}</span>
            </li>
    </ul>
    <p v-else>
      Nenhuma tarefa cadastrada.
    </p>
  </div>
</template>

<script>
import { Task } from './classes/Task.js';

export default {
  name: 'app',

  data() {
    return {
      tasks: [
        new Task('Estudar REA'),
        new Task('Exercícios REA'),
        new Task('Trabalho REA'),
        new Task('Assistir aulas REA'),
      ],
    };
  },

  methods: {
    newTask: function(event) {
      const taskDescription = event.target.value.trim();

      /**
       * Verificamos se realmente podemos incluir a
       * nova tarefa
       */
      if (!this._canAddTask(taskDescription)) return;

      this.tasks = [...this.tasks, new Task(taskDescription)];
    },

    /**
     * Verifica a possibilidade da inclusão da tarefa
     * com base nas seguintes regras:
     *
     * 1) Tarefa existente
     * 2) Descrição ainda não existe na listagem de tarefas
     */
    _canAddTask: function(taskDescription) {
      return (
        !!taskDescription &&
        this.tasks.filter(task => task.description === taskDescription).length === 0
      );
    },

    /**
     * Completando a tarefa
     */
    completeTask(task) {
      task.completeTask();
    },

    /**
     * Excluindo a tarefa
     */
    removeTask(task) {
      this.tasks.splice(this.tasks.indexOf(task), 1);
    },
  },
};
</script>

<style>
body {
  padding: 20px;
}

.completed {
  color: green;
  font-weight: bold;
}
</style>
