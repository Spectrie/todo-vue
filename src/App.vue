<script setup>
  import { reactive } from 'vue';
  import Cabecalho from './components/Cabecalho.vue';
  import Formulario from './components/Formulario.vue';
  import ListaDeTarefas from './components/ListaDeTarefas.vue';
  const estado = reactive({
    tarefaTemporaria: '',
    filtro : 'todas',
    tarefas: [
      {
        titulo: 'Estudar ES6',
        finalizada: false,
      },
      {
        titulo: 'Estudar SASS',
        finalizada: false,
      },
      {
        titulo: 'Ir para a academia',
        finalizada: true,
      }
    ]
  })
  const getTarefasPendentes = () =>{
    return estado.tarefas.filter(tarefa => tarefa.finalizada ===false)
  }
  const getTarefasFinalizadas = () =>{
    return estado.tarefas.filter(tarefa => tarefa.finalizada ===true)
  }
  const getTarefasFiltradas =() =>{
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
  const cadastraTarefa = () =>{
    const tarefaNova = {
      titulo: estado.tarefaTemporaria,
      finalizada: false
    }
    estado.tarefas.push(tarefaNova);
    estado.tarefaTemporaria = '';
  }
</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length"/>
    <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefa-temporaria="estado.tarefaTemporaria" :edita-tarefa-temp="evento => estado.tarefaTemporaria = evento.target.value" :cadastra-tarefa="cadastraTarefa"/>
    <ListaDeTarefas :tarefas="getTarefasFiltradas()"/>  
  </div>
</template>


