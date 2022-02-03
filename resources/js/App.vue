<template>
    <div id="app">
        <div id="todo">
            <h1 class="text-center fw-bold">Todo App</h1>
            <add-item @loadTasks="getAllTask()" />
            <list-item :tasks="tasks" @loadTasks="getAllTask()" />
        </div>
    </div>
</template>
<script>
import AddItem from "./components/AddItem.vue";
import ListItem from "./components/ListItem.vue";
export default {
    data() {
        return {
            tasks: [],
        };
    },
    components: {
        AddItem,
        ListItem,
    },
    created() {
        this.getAllTask();
    },
    methods: {
        getAllTask() {
            axios
                .get("http://127.0.0.1:8000/api/todo")
                .then((response) => {
                    // response.data.data = this.tasks;
                    this.tasks = response.data;
                })
                .catch((e) => {
                    console.log(e);
                });
        },
    },
};
</script>
<style scoped lang="scss">
#app {
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: aqua;
    min-height: 100vh;
    #todo {
        min-height: 300px;
        background-color: #fff;
        width: 600px;
        padding: 20px 30px;
    }
}
</style>
