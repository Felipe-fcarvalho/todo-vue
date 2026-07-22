<script setup>
import { reactive, computed } from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import ListaDeTarefas from './components/ListaDeTarefas.vue';

const estado = reactive({
  filtro: 'todas',
  tarefaTemp: '',
  tarefas: [
    { id: 1, titulo: 'Estudar ES6', finalizada: false },
    { id: 2, titulo: 'Estudar SASS', finalizada: false},
    { id: 3, titulo: 'Academia', finalizada: true},
  ]
})

const tarefasPendentes = computed(() => estado.tarefas.filter(tarefa => !tarefa.finalizada))

const tarefasFinalizadas = computed(() => estado.tarefas.filter(tarefa => tarefa.finalizada))

const tarefasFiltradas = computed(() => {
  switch (estado.filtro) {
    case 'pendentes': 
      return tarefasPendentes.value;
    case 'finalizadas':
      return tarefasFinalizadas.value;
    default:
      return estado.tarefas
  }
})

const cadastraTarefa = () => {
  const titulo = estado.tarefaTemp.trim()
  if(!titulo) return
  
  const tarefaNova = {
    id: Date.now(),
    titulo,
    finalizada: false,
  }

  estado.tarefas.push(tarefaNova);
  estado.tarefaTemp = '';
}
</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="tarefasPendentes.length"/>
    <Formulario 
      :tarefa-temp="estado.tarefaTemp" 
      :filtro="estado.filtro"
      @atualiza-tarefa="valor => estado.tarefaTemp = valor"
      @muda-filtro="valor => estado.filtro = valor" 
      @submit-tarefa="cadastraTarefa"
    />
    <ListaDeTarefas :tarefas="tarefasFiltradas"/>
  </div>
</template>


