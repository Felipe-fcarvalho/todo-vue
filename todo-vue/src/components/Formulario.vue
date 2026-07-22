<script setup>
const props = defineProps({
    tarefaTemp: String,
    filtro: String
})

const emit = defineEmits(['atualiza-tarefa', 'muda-filtro', 'submit-tarefa'])
</script>

<template>
    <form @submit.prevent="emit('submit-tarefa')">
        <div class="row">
            <div class="col">
                <input 
                    :value="props.tarefaTemp" 
                    @input="emit('atualiza-tarefa', $event.target.value)" 
                    required 
                    class="form-control" 
                    type="text" 
                    placeholder="Digite aqui a descrição da tarefa">
            </div>
            <div class="col-md-2">
            <button class="btn btn-primary" type="submit">Cadastrar</button>
            </div>
            <div class="col-md-2">
            <select :value="props.filtro" @change="emit('muda-filtro', $event.target.value)" class="form-control">
                <option value="todas">Todas tarefas</option>
                <option value="pendentes">Tarefas pendentes</option>
                <option value="finalizadas">Finalizadas</option>
            </select>
            </div>
        </div>
    </form>
</template>