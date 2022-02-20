<template>
  <div class="container">
    <div class="row">
      <!-- //col-sm-4 .d-print-flex -->
      <div class="col-auto" v-for="task in tasks" :key="task.id">
        <div
          class="card text-white bg-dark mb-3 border border-white"
          style="width: 18rem">
          <div class="card-body">
            <p>
              <label :class="{ tachado: task.isCompleted }"
                >Id: {{ task.id }}</label
              >
            </p>
            <p>
              <label :class="{ tachado: task.isCompleted }"
                >Tarefa: {{ task.task }}</label
              >
            </p>
            <label :class="{ tachado: task.isCompleted }">
              Finalizada:
              <input
                :checked="task.isCompleted"
                type="checkbox"
                @click="tachado(task.id)"
              />
            </label>
            <p>
              <button
                v-on:click="removeTask(task.id)"
                class="
                  btn btn-secondary btn-sm
                  border border-white
                  botao_apagar
                "
                data-bs-toggle="modal" data-bs-target="#exampleModal"
              >
                Apagar
              </button>
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ListaTarefas",
  props: {
    tasks: [],
  },
  data() {
    return {
      tasksArray: []
    };
  },
  methods: {
    tachado(taskId) {
      for (const task of this.tasks) {
        if (task.id === taskId) {
          task.isCompleted = !task.isCompleted;
        }
      }
    },

    removeTask(taskId) {
      this.$emit('clicked', taskId)
    },
  },
};
</script>

<style scoped>

ul {
  list-style: none;
}
.card {
  margin-bottom: 0.5em;
  border-radius: 10px;
  font-weight: 600;
  opacity: 0.9;
}
.card:hover{
  opacity: 1;
  -moz-transform: scale(1.05);
	-webkit-transform: scale(1.05);
	transform: scale(1.05);
  transition: all 0.5s;
}

.container {
  color: #BFBFBF;
  padding: 5em;
  padding-top: 1em;
  border-radius: 10px;
  display: flex;
  justify-content: center;
}
.tachado {
  text-decoration: line-through;
  opacity: 0.5;
}
.naotachado {
  text-decoration: none;
}
.botao_apagar {
  margin-top: 5px;
}
</style>