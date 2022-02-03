<template>
    <div id="list">
        <div class="item-list mb-3" v-for="(task, index) in tasks" :key="index">
            <item-list :task="task" @loadTasks="$emit('loadTasks')" />
        </div>
    </div>
</template>
<script>
import ItemList from "./ItemList.vue";
export default {
    props: ["tasks"],
    components: {
        ItemList,
    },
    watch: {},
    methods: {},
};
</script>
<style scoped lang="scss">
#list {
    margin-top: 30px;
    .item-list {
        padding: 8px 30px;
        border: 1px solid #ccc;
    }
}
</style>
