<script setup>
  // const nome = "Liyiling";
  // const fofo = "https://img.freepik.com/vetores-gratis/bebe-fofo-panda-hug-bamboo-cartoon-vector-icon-ilustracao-conceito-de-icone-de-natureza-animal-isolado_138676-5564.jpg?w=740&t=st=1677359567~exp=1677360167~hmac=b2fa642435081cf93c66f3615acfdefff4d89634fe0e4ac6e6b64a7a2840ad61"
  // const fofo2 = "https://static.vecteezy.com/ti/vetor-gratis/p3/3226499-desenho-de-patinho-fofo-e-feliz-vetor.jpg"
  // shift alt f
  import { reactive } from 'vue';
  import Cabecalho from './components/Cabecalho.vue';
  import Formulario from './components/Formulario.vue';
  import ListaDeTarefa from './components/ListaDeTarefas.vue';

  // const verSegundafOTO = true

  const estado = reactive({
    filtro: "todas",
    tarefaTemp: '',
    tarefas: [
      {
        titulo: "Estudar", 
        finalizada: false
      },
      {
        titulo: "Comprar", 
        finalizada: false
      },
      {
        titulo: "Sair", 
        finalizada: true
      }
    ]
  })

  const getTarefaPnedentes = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizada === false)
  }

  const getTarefasPendentes = () => {
    return estado.tarefas.filter(tarefa => !tarefa.finalizada)
  }

  const getTarefasFinalizadas = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizada)
  }

  const getTarefasFiltradas = () => {
    const {filtro} = estado;
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
    // e.preventDefault();
    const tarefaNova = {
      titulo: estado.tarefaTemp,
      finalizafa: false,
    }
    estado.tarefas.push(tarefaNova);
    estado.tarefaTemp = '';
  }

</script>

<template>

  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />
    <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastra-tarefa="cadastraTarefa" />
    <ListaDeTarefa :tarefas="getTarefasFiltradas()" />
  </div>
  
  <!-- <h1>ola nmu {{nome}}</h1>
  <br>
  <img v-bind:src=" fofo " alt="">
  <img v-if="verSegundafOTO" :src=" fofo2 " alt="" style="width: 500px;"> -->
  
</template>


<style scoped>
  .done{
    text-decoration: line-through;
  }
</style>
