<template>
  <AppHeader />
  <div class="espaço"></div>
  <PreencherTask 
  @adicionar="gerar_tarefa" />
  
  <BaseTask 
  v-for="(tarefa, index) in tarefas" 
  :key="index" titulo="Tarefa criada" 
  :entrada="tarefa"
  @deletar="deletar_tarefa(index)" @marcar="marcar_tarefa(index)" />

</template>

<script>
import AppHeader from './components/AppHeader.vue'
import PreencherTask from './components/PreencherTask.vue';
import BaseTask from './components/BaseTask.vue'
import './assets/base.css';
export default {
  components: {
    AppHeader,
    BaseTask,
    PreencherTask
  },

  data() {
    return {
      tarefas: [],
      animar: false
    }
  },

  mounted() {
    const tarefasSalvas = localStorage.getItem('tarefas');

    if (tarefasSalvas) {
      this.tarefas = JSON.parse(tarefasSalvas);
    }
  },

  methods: {
    gerar_tarefa(texto) {
      this.tarefas.push({
        texto
      });
    },

    deletar_tarefa(index) {
      this.tarefas.splice(index, 1);
    },

    marcar_tarefa(index) {
      this.tarefas[index].feita = !this.tarefas[index].feita;
    }
  },

  watch: {
    tarefas: {
      handler(tarefas) {
        localStorage.setItem('tarefas', JSON.stringify(tarefas));
      },
      deep: true
    }
  }
}
</script>

<style>

.titulo {
  letter-spacing: 0.08em;
  font-weight: 400;
}

.titlehometech {
  letter-spacing: 0.15em;
}

.espaço {
  margin-top: 100px;
}

</style>
