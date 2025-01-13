<script setup>
import { reactive } from 'vue';
import Cabecalho from './componentes/Cabecalho.vue';
import Formulario from './componentes/Formulario.vue';
import ListaDaTarefas from './componentes/ListaDaTarefas.vue';


const estado = reactive({
  filtro: 'todas',
  tarefaTemp: '',

  tarefas: [
    {
      titulo: 'Estudar ES6',
      finalizadas: false,
    },
    {
      titulo: 'Estudar SASS',
      finalizadas: false,
    },
    {
      titulo: 'Ir para a academia',
      finalizadas: true,
    }
  ]
})

const getTarefasPendentes = () => {
   return estado.tarefas.filter(tarefa => !tarefa.finalizada)
}

const getTarefasFinalizadas = () => {
   return estado.tarefas.filter(tarefa => tarefa.finalizada)
}

const getTarefasFiltradas = () => {
  const {filtro} = estado;

  switch (filtro) {
    case 'pendents' :
      return getTarefasPendentes();
    case 'finalizadas' :
      return getTarefasFinalizadas();
      default :
      return estado.tarefas;
  }
}

const cadastraTarefa = (e) => {
  e.preventDefault();
  const tarefaNova = {
    titulo: estado.tarefaTemp,
    finalizada: false,
  }
  estado.tarefas.push(tarefaNova);
  estado.tarefaTemp = '';

}
</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length"/>
    <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefa-temp="estado.tarefaTemp" :editar-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastra-tarefa="cadastraTarefa"/>
    <ListaDaTarefas :tarefas="getTarefasFiltradas()"/>
  </div>
</template>


