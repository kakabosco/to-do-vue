<script setup>
    import { reactive } from "vue";

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
                return getPendingTasks();
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
        <header class="p-5 mb-4 mt-4 bg-light rounded-3">
            <h1>Minhas tarefas</h1>
            <p v-if="getPendingTasks().length > 0">
                Você possui {{ getPendingTasks().length }} tarefas pendentes
            </p>
            <p v-else>Você não possui tarefas pendentes</p>
        </header>
        <form @submit.prevent="registerTask">
            <div class="row">
                <div class="col">
                    <input
                        :value="state.tempTask"
                        @change="(e) => (state.tempTask = e.target.value)"
                        required
                        type="text"
                        placeholder="Nova tarefa"
                        class="form-control" />
                </div>
                <div class="col-md-2">
                    <button type="submit" class="btn btn-primary">
                        Adicionar
                    </button>
                </div>
                <div class="col-md-2">
                    <select @change="changeFilter" class="form-select">
                        <option value="all">Todas</option>
                        <option value="pending">Pendentes</option>
                        <option value="finished">Finalizadas</option>
                    </select>
                </div>
            </div>
        </form>
        <ul class="list-group mt-4">
            <li class="list-group-item" v-for="task in getFilteredTasks()">
                <input
                    @change="(e) => (task.done = e.target.checked)"
                    :checked="task.done"
                    :id="task.title"
                    type="checkbox"
                    name=""
                    id="" />
                <label
                    :class="{ done: task.done }"
                    class="ms-3"
                    :for="task.title">
                    {{ task.title }}
                </label>
            </li>
        </ul>
    </div>
</template>

<style scoped>
    .done {
        text-decoration: line-through;
        color: #aaa;
    }

    select {
        cursor: pointer;
    }
</style>

