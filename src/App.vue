<template>
  <div class="container">
    <div class="form">
      <h1>{{ title }}</h1>
      <input type="text" v-model.trim="item" v-on:keyup.enter="AddTask" class="input"/>
      <button @click="AddTask" class="btn btn-outline-dark border border-white botao">Adicionar</button>
    </div>
    <Tasks :tasks="tasks" @clicked="removeTaskChild"></Tasks>
  </div>
</template>

<script>
import Tasks from "./components/Tasks.vue";
export default {
  name: "App",
  components: {
    Tasks,
  },
  data() {
    return {
      title: "Lista de Tarefas",
      item: "",
      tasks: [
        { id: 1, task: "1º Tarefa", isCompleted: true },
        { id: 2, task: "2º Tarefa", isCompleted: false },
        { id: 3, task: "3º Tarefa", isCompleted: true },
      ],
    };
  },
  methods: {
    AddTask() {
      console.log(this.item);
      this.tasks.push({
        id: this.GetLastId(),
        task: this.item,
        isCompleted: false,
      });
      this.item = ''
    },
    removeTaskChild(value){
      for (let i = 0; i < this.tasks.length; i++) {
        let task = this.tasks[i];
        if (task.id === value) {
          this.tasks.splice(i, 1);
          break;
        }
      }
    },
    GetLastId() {
      if(this.tasks.length > 0){
        let task = this.tasks[this.tasks.length - 1];
        return task.id + 1;
      }
      else
        return 1
    },
  },
};
</script>

<style>
h1{
  font-weight: 700;
  margin-bottom: 40px;
}
body{
  /* background-color: #7D6AA6; */
  background-color: #A988F2;
}
#app {

  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
  padding-top: 30px;
  display: flex;
  justify-content: center;
}
.container{
  display: flexbox;
  justify-content: center;
}
.form {
  margin-bottom: 3em;
}
.input{
  margin-right: 0.2em;
  margin-bottom: 0.5em;
  border-radius: 5px;
  padding: 4px;
  width: 300px;
}
.botao{
  color: #ffffffef;
}
.botao:hover{
  color: white;
  transition: all 0.3s;
}
</style>
