<template>
    <div class="form-check">
        <input
            type="checkbox"
            class="form-check-input"
            @change="updateTask"
            v-model="task.completed"
        />
        <span class="form-check-label" v-if="!isEdit">{{ task.name }}</span>
        <input
            type="text"
            class="edit"
            v-if="isEdit"
            v-model="task.name"
            autofocus
        />
        <div class="icon">
            <span v-if="!isEdit" @click="editTask()"
                ><i class="fas fa-edit"></i
            ></span>
            <span v-if="!isEdit" @click="deleteTask()"
                ><i class="fas fa-window-close"></i
            ></span>
            <span v-if="isEdit" @click="updateTask()"
                ><i class="fa fa-check" aria-hidden="true"></i
            ></span>
        </div>
    </div>
</template>
<script>
import axios from "axios";
export default {
    props: ["task"],
    data() {
        return {
            isEdit: false,
            isSelected: 0,
            editName: "",
        };
    },
    watch: {},
    methods: {
        editTask() {
            this.isEdit = true;
            this.focus = true;
        },
        updateTask() {
            axios
                .put("http://127.0.0.1:8000/api/todo/" + this.task.id, {
                    name: this.task.name,
                    completed: this.task.completed,
                })
                .then(() => {
                    this.$emit("loadTasks");
                })
                .catch((e) => {});
            this.isEdit = false;
        },
        deleteTask() {
            axios
                .delete("http://127.0.0.1:8000/api/todo/" + this.task.id)
                .then(() => {
                    this.$emit("loadTasks");
                })
                .catch((e) => {});
        },
    },
};
</script>
<style scoped lang="scss">
.form-check {
    input[type="text"] {
        border: none;
        border-bottom: 1px solid #ccc;
        width: 80%;
        &:focus {
            outline: none;
        }
    }
    input[type="checkbox"] {
        &:checked + {
            .form-check-label {
                text-decoration: line-through;
            }
        }
    }
}

.icon {
    display: block;
    float: right;
    i {
        font-size: 20px;
        margin-left: 10px;
        cursor: pointer;
        &:hover {
            color: rgb(233, 68, 131);
        }
    }
}
</style>
