<script setup>

    const props = defineProps(['cadastraTarefa', 'tarefaTemporaria', 'trocarFiltro', 'editaTarefaTemporaria']);

</script>


<template>

    <form @submit.prevent="props.cadastraTarefa">

        <div class="row">

            <div class="col">
                <input :value="props.tarefaTemporaria"
                    @change="props.editaTarefaTemporaria" required type="text"
                    placeholder="Digite a descrição da tarefa" class="form-control">
            </div>

            <div class="col-md-2">
                <button class="btn btn-primary" type="submit">Cadastrar</button>
            </div>

            <div class="col-sm-4 col-lg-2">
                <select class="form-control form-select" @change="props.trocarFiltro">
                    <option value="todas">Todas tarefas</option>
                    <option value="pendentes">Pendentes</option>
                    <option value="finalizadas">Finalizadas</option>
                </select>
            </div>

        </div>

    </form>

</template>