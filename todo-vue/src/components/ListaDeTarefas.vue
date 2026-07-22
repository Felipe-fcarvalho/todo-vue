<script setup>
const props = defineProps({ tarefas: Array })
</script>

<template>
    <ul class="list-group mt-4">
        <li class="list-group-item" v-for="tarefa in props.tarefas" :key="tarefa.id">
            <input 
                v-model="tarefa.finalizada" 
                type="checkbox" 
                :id="`tarefa-${tarefa.id}`"
            >
            <label 
                :class="{ done: tarefa.finalizada }" 
                class="ms-3" 
                :for="`tarefa-${tarefa.id}`"
            >
                {{ tarefa.titulo }}
            </label>
        </li>
    </ul>
</template>

<style scoped>
    .done {
        text-decoration: line-through;
    }
</style>