<script setup>
  import { reactive } from 'vue';
  import Cabecalho from './components/cabecalho.vue';
  import Formulario from './components/Formulario.vue';
  import ListaDeTarefas from './components/ListaDeTarefas.vue';


const estado = reactive({
  filtro: 'todas',
  tarefaTemp: '',
  tarefas: [{
    titulo: 'estudar ES6',
    finalizada: false
  },
  {
    titulo: 'estudar sass',
    finalizada: false
  },
  {
    titulo: 'academia',
    finalizada: true
  }
  ]
})

const getTarefasPendentes = () => {
  return estado.tarefas.filter(tarefa => !tarefa.finalizada)
}

const getTarefasFinalizadas = () => {
  return estado.tarefas.filter(tarefa => tarefa.finalizada)
}

const getTarefas = () => {
  const { filtro } = estado;
  switch (filtro) {
    case 'pendentes':
      return getTarefasPendentes();
    case 'finalizadas':
      return getTarefasFinalizadas();
    default:
      return estado.tarefas;
  }
}

const cadastraTarefa = () => {
  const tarefaNova = {
    titulo: estado.tarefaTemp,
    finalizada: false,
  }
  estado.tarefas.push(tarefaNova);
  estado.tarefaTemp = '';
}

const verificar = () => {
    return estado.tarefas.length > 0;
  }

</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />
    <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastra-tarefa="cadastraTarefa"/>
    <ListaDeTarefas v-if="verificar()" :tarefas="getTarefas()"/>
    <div v-else>
      <p>nao tem nenhum item na lista</p>
    </div>

  </div>
</template>

