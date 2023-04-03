<script setup>
import { reactive } from 'vue';

const estado = reactive({
  filtro: 'todas',
  tarefas: [
    {
      titulo: 'Estudar ES6',
      finalizada: false,
    }, 
    {
      titulo: 'Estudar SAS',
      finalizada: false,
    },
    {
      titulo: 'Ir para academia',
      finalizada: true,
    }
  ]
})

const getTarefasPendentes = () => {
  return estado.tarefas.filter(tarefa => !tarefa.finalizada)
}

</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas Tarefas</h1>
      <p>Você possui {{ getTarefasPendentes().length }} tarefas pendentes</p>
    </header>
  </div>
  <form>
    <div class="row">
      <div class="col">
        <input type="text" placeholder="Digite aqui a descrição da tarefa" class="form-control" >
      </div>
      <div class="col-md-2">
        <button type="submit" class="btn btn-primary">Cadastrar</button>
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
  {{ estado.filtro }}
  <ul class="list-group mt-4">
    <li class="list-group-item" v-for="tarefa in estado.tarefas">
      <input type="checkbox" :checked="tarefa.finalizada" :id="tarefa.titulo">
      <label :class="{ done: tarefa.finalizada }" class="ms-3" :for="tarefa.titulo">
        {{tarefa.titulo}}
      </label>
    </li>
  </ul>
</template>

<style scoped>
.done{
  text-decoration: line-through;
}

</style>
