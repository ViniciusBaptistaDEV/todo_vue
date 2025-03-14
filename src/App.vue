<script setup>

import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import ListaDeTarefas from './components/ListaDeTarefas.vue';


const estado = reactive({
  filtro: 'todas',
  tarefaTemporaria: '',
  tarefas: []
})

const getTarefasPendentes = () => {
  return estado.tarefas.filter(tarefa => tarefa.finalizada === false)
}

const getTarefasFinalizadas = () => {
  return estado.tarefas.filter(tarefa => tarefa.finalizada === true)
}

const getTarefasFiltradas = () => {
  const filtro = estado.filtro;

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
    titulo: estado.tarefaTemporaria,
    finalizada: false
  }

  estado.tarefas.push(tarefaNova);
  estado.tarefaTemporaria = '';
}

function getMensagemVazia() {
  if (estado.filtro === 'todas') {
    return "Você não tem nenhuma tarefa cadastrada.";
  } else if (estado.filtro === 'pendentes') {
    return "Você não tem nenhuma tarefa pendente.";
  } else if (estado.filtro === 'finalizadas') {
    return "Você não tem nenhuma tarefa finalizada ainda.";
  }
}

</script>

<template>

  <div class="container">

    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />
    <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefa-temporaria="estado.tarefaTemporaria" :edita-tarefa-temporaria="evento => estado.tarefaTemporaria = evento.target.value" :cadastra-tarefa="cadastraTarefa" />
    <ListaDeTarefas :tarefas="getTarefasFiltradas()" :filtro-if="getMensagemVazia()"  />

  </div>

</template>


