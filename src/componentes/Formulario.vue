<script setup>
  const props = defineProps(['cadastraTarefa', 'tarefaTemp', 'trocarFiltro', 'editarTarefaTemp'])
</script>
<template>
    <form @submit="props.cadastraTarefa">
    <div class="row">
      <div class="col">
        <input :value="props.tarefaTemp" @change="props.editarTarefaTemp" required type="text" placeholder="Digite aqui a descricao da tarefa" class="form-control">
      </div>
      <div class="col-md-2">
        <button type="submit" class="btn btn-primary">Cadastrar</button>
      </div>
      <div class="col-md-2">
        <select @change="props.trocarFiltro" class="form-control">
          <option value="todas">Todos tarefas</option>
          <option value="pendentes">Pendentes</option>
          <option value="finalizadas">Finalizadas</option>
        </select>
      </div>
    </div>
  </form>
</template>