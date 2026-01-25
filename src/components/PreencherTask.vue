<template>

    <div>

        <form @submit.prevent="verificar">

            <input type="text" id="tarefa" 
            placeholder="Digite a tarefa que você quer listar" 
            v-model="entrada" />
            
            <button type="button" class="buttonAdicionar" @click="verificar">Adicionar</button>

        </form>

    </div>
    
    <div v-if="alerta" class="espacoDivErro">
        <div  class="diverro">
            
            <p class="erro">{{ alerta }}</p>
            <button class="buttonErro" @click="fechar">OK</button>
        
        </div>
    </div>
</template>

<script>

export default {
    data() {
        return {
            entrada: '',
            alerta: ''
        }
    },

    methods: {
        verificar() {
            let limite = 60;

            if (this.entrada.length > limite) {
                this.alerta = `A tarefa não pode ter mais que ${limite} caracteres.`;
                this.entrada = '';
                return;
            } else {
                this.alerta = '';
                this.add_task();
                }
        },

        fechar() {
            this.alerta = '';
        },

        add_task() {
            if (this.entrada.trim() === '') {
                return;
            }
            this.$emit('adicionar', this.entrada);
            this.entrada = '';
        }
    }
}

</script>

<style scoped>

div {
    display: flex;
    width: 100%;
    align-items: center;
    justify-content: center;
}

.buttonAdicionar {
    padding: 10px;
    border: solid 2px rgba(255, 255, 255, 0.627);
    border-bottom-right-radius: 6px;
    border-top-right-radius: 6px;
    border-left: solid 1px rgb(255, 255, 255, 0.627);
    transition: 0.3s;
}

.buttonErro {
    border-radius: 6px;
    margin-bottom: auto;
    margin-right: 0%;
    padding: 10px;
    transition: 0.3s;
    color: white;
    background-color: rgb(17, 17, 17);
}

.espacoDivErro {
    display: flex;
    position: fixed;
    justify-content: center;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
}

.diverro {
  background-color: #161616;
  color: white;
  border-radius: 6px;
  border: solid 2px rgba(240, 248, 255, 0.627);
  font-size: 14px;
  height: 2cm;
  width: 12cm;
  display: flex;
  text-align: center;
  font-size: 17px;
}

.erro {
    margin: auto;
    padding: 20px;
}

@media (hover: hover) {

    .buttonErro:hover {
        color: black;
        background-color: hsl(0, 0%, 100%);
        cursor: pointer;
    }

    .buttonAdicionar:hover {
        color: black;
        background-color: hsl(0, 0%, 100%);
        cursor: pointer;
    }
    
}
</style>