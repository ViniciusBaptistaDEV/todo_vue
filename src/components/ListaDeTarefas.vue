<script setup>

const props = defineProps(['tarefas', 'filtroIf']);

</script>

<template>

    <ul v-if="props.tarefas.length > 0" class="list-group mt-4">
        <li class="list-group-item" v-for="tarefa in props.tarefas">
            <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada"
                :id="tarefa.titulo" type="checkbox">
            <label :class="{ done: tarefa.finalizada }" class="ms-3" :for="tarefa.titulo">
                {{ tarefa.titulo }}
            </label>
        </li>
    </ul>
    <h5 v-else class="mt-5">
        {{ props.filtroIf }}
    </h5>

</template>

<style scoped>
    .done {
        text-decoration: line-through;
    }
</style>