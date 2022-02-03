<template>
    <div>
        <div class="form-group d-flex">
            <input
                type="text"
                name="name"
                id="name"
                class="form-control"
                placeholder="add todo"
                aria-describedby="helpId"
                v-model="item.name"
            />
            <button type="button" class="btn btn-primary" @click="addItemList">
                +
            </button>
        </div>
    </div>
</template>
<script>
import axios from "axios";
export default {
    data() {
        return {
            item: {
                name: null,
            },
        };
    },
    methods: {
        addItemList() {
            axios
                .post("http://127.0.0.1:8000/api/todo", this.item)
                .then((response) => {})
                .catch((e) => {});
            this.item.name = null;
            this.$emit("loadTasks");
        },
    },
};
</script>
<style scoped lang="scss">
button {
    margin-left: 5px;
}
</style>
