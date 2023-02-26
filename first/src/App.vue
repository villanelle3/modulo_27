<script setup>
  // const nome = "Liyiling";
  // const fofo = "https://img.freepik.com/vetores-gratis/bebe-fofo-panda-hug-bamboo-cartoon-vector-icon-ilustracao-conceito-de-icone-de-natureza-animal-isolado_138676-5564.jpg?w=740&t=st=1677359567~exp=1677360167~hmac=b2fa642435081cf93c66f3615acfdefff4d89634fe0e4ac6e6b64a7a2840ad61"
  // const fofo2 = "https://static.vecteezy.com/ti/vetor-gratis/p3/3226499-desenho-de-patinho-fofo-e-feliz-vetor.jpg"

import { reactive } from 'vue';

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
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas Tarefas</h1>
      <p>
        Você possui {{ getTarefasPendentes().length }} tarefas pendentes.
      </p>
    </header>
    <form action="" @submit.prevent="cadastraTarefa">
      <div class="row">
        <div class="col">
          <input :value="estado.tarefaTemp" @change="evento => estado.tarefaTemp = evento.target.value" required type="text" placeholder="Descrição da tarefa" class="form-control">
        </div>
        <div class="col-md-2">
          <button class="btn btn-primary" type="submit">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select @change="evento => estado.filtro = evento.target.value" class="form-control">
            <option value="todas">Todas as tarefas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
        <input @change="elemento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
        <label :for="tarefa.titulo" class="ms-3" :class="{ done: tarefa.finalizada === true }">
          {{ tarefa.titulo }}
        </label>
      </li>
    </ul>
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
