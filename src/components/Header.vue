<script setup>
    const props = defineProps(["pendingTasks"]);
</script>
<template>
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
        <h1>Minhas tarefas</h1>
        <p v-if="props.pendingTasks > 0">
            Você possui {{ props.pendingTasks }} tarefas pendentes
        </p>
        <p v-else>Você não possui tarefas pendentes</p>
    </header>
</template>
