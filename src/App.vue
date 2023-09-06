<script setup>
    import { reactive } from "vue";
    import Header from "./components/Header.vue";
    import Form from "./components/Form.vue";
    import List from "./components/List.vue";

    const state = reactive({
        filter: "all",
        tempTask: "",
        tasks: [
            {
                title: "Tarefa 1",
                done: false,
            },
            {
                title: "Tarefa 2",
                done: false,
            },
            {
                title: "Tarefa 3",
                done: true,
            },
        ],
    });

    const getPendingTasks = () => {
        return state.tasks.filter((task) => !task.done);
    };

    const getFinishedTasks = () => {
        return state.tasks.filter((task) => task.done);
    };

    const getFilteredTasks = () => {
        const { filter } = state;

        switch (filter) {
            case "pending":
                return getPendingTasks().length > 0 ? getPendingTasks() : null;
            case "finished":
                return getFinishedTasks();
            default:
                return state.tasks;
        }
    };

    const registerTask = () => {
        const newTask = {
            title: state.tempTask,
            done: false,
        };
        state.tasks.push(newTask);
        state.tempTask = "";
    };

    function changeFilter(e) {
        state.filter = e.target.value;
    }
</script>

<template>
    <div class="container">
        <Header :pending-tasks="getPendingTasks().length" />
        <Form
            :change-filter="changeFilter"
            :temp-task="state.tempTask"
            :edit-temp-task="(e) => (state.tempTask = e.target.value)"
            :register-task="registerTask" />
        <List :tasks="getFilteredTasks()" />
    </div>
</template>

