<template>

  <div class="grade">
    <div class="card" :class="{ animate: entrada.feita }">
      <h2>{{ titulo }}</h2>

      <div class="taskEBotoes">
        <p>Tarefa: {{ entrada.texto }}</p>

        <button type="button" class="check" @click="marcar"><img src="../assets/icons/check-fat-bold.svg"></button>
        <button type="button" class="trash" @click="delet"><img src="../assets/icons/trash-bold.svg"></button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    titulo: String,
    entrada: String
  },
  methods: {
    delet() {
      this.$emit('deletar');
    },
    marcar() {
      this.$emit('marcar');
    }
  }
}

</script>

<style scoped>

.taskEBotoes {
  display: flex;
  align-items: center;
  height: 20px;
}

.taskEBotoes button:first-of-type {
  margin-left: auto;
}

.taskEBotoes .check:first-of-type:hover {
  transition: 0.1s;
  background-color: rgb(110, 183, 0);
  scale: 1.1;
  cursor: pointer;
}

.taskEBotoes .trash:last-of-type:hover {
  transition: 0.1s;
  background-color: rgb(183, 0, 0);
  scale: 1.1;
  cursor: pointer;
}

h2 {
  height: 15px;
  margin-top: 3px;
}

.animate {
  animation: moveAround 0.3s;
  animation-fill-mode: forwards;
}

@keyframes moveAround {
  0% {
    background-color: rgb(17, 17, 17);
    scale: 1
  }
  50% {
    background-color: rgb(34, 139, 34);
    border: solid 2px rgb(255, 255, 255);
    scale: 1.05
  }
  100% {
    background-color: rgb(34, 139, 34);
    border: solid 2px rgb(255, 255, 255);
    scale: 1
  }
}


.check, .trash {
  background-color: rgba(240, 248, 255, 0);
  border: 2px solid rgb(189, 189, 189);
  border-radius: 8px;
  width: 60px;
  margin: 2px;
}

</style>