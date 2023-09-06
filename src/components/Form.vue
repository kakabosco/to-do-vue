<script setup>
    const props = defineProps([
        "registerTask",
        "tempTask",
        "changeFilter",
        "editTempTask",
    ]);
</script>

<template>
    <form @submit.prevent="props.registerTask">
        <div class="row">
            <div class="col">
                <input
                    :value="props.tempTask"
                    @change="props.editTempTask"
                    required
                    type="text"
                    placeholder="Nova tarefa"
                    class="form-control" />
            </div>
            <div class="col-md-2">
                <button type="submit" class="btn btn-primary">Adicionar</button>
            </div>
            <div class="col-md-2">
                <select @change="props.changeFilter" class="form-select">
                    <option value="all">Todas</option>
                    <option value="pending">Pendentes</option>
                    <option value="finished">Finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>

<style scoped>
    select {
        cursor: pointer;
    }
</style>
