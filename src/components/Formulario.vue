<script setup>
    const props =defineProps(['cadastraTarefa','tarefaTemp','trocarFiltro','editaTarefaTemp'])
</script>
<template>
    <form @submit.prevent="props.cadastraTarefa">
        <div class="row">
            <div class="col">
                <input :value="props.tarefaTemp" @change="props.editaTarefaTemp" required
                    type="text" placeholder="digite a descrição da tarefa" class="form-control" />
                <!-- change e quando o usuario tem que sair do campo para fazer uma outra ação ja o keyup ele nao precisa sair do campo-->

            </div>
            <div class="col-md-2">
                <button class="btn btn-primary" type="submit">
                    Cadastrar
                </button>
            </div>
            <div class="col-md-2">
                <select @change="props.trocarFiltro" class="form-control">
                    <option value="todas">Todas tarefas</option>
                    <option value="pendentes">Pendenes</option>
                    <option value="finalizadas">Finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>