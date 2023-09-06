<script setup>
    const props = defineProps(["tasks"]);
</script>

<template>
    <ul class="list-group mt-4" v-if="props.tasks !== null">
        <li class="list-group-item" v-for="task in props.tasks">
            <input
                @change="(e) => (task.done = e.target.checked)"
                :checked="task.done"
                :id="task.title"
                type="checkbox"
                name=""
                id="" />
            <label :class="{ done: task.done }" class="ms-3" :for="task.title">
                {{ task.title }}
            </label>
        </li>
    </ul>
    <p class="mt-2 ms-2 fw-bold" v-else>Não há tarefas pendentes</p>
</template>

<style scoped>
    .done {
        text-decoration: line-through;
        color: #aaa;
    }
</style>
