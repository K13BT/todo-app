<template>
    <div class="todo" @mouseover="showDelete" @mouseleave="hideDelete">
        <button @click="$emit('toggleTodoComplete', todo.id)" :class="todo.isCompleted ? 'completed-check' : 'checkbox'" >
        <img v-show="todo.isCompleted" src="../assets/images/icon-check.svg" />
        </button>
        <p :class="modeCompleted">
        {{ todo.text }}
        </p>
        <button class="btn-delete" @click="$emit('deleteTodo', todo.id)" v-if="isDeleteVisible">
            <img src="../assets/images/icon-cross.svg" />
        </button>
    </div>
</template>


<script>
    export default {
        name: 'SingleTodo',
        props: {
            todo: Object,
            darkMode: Boolean
        },
        data() {
            return {
                isDeleteVisible: false
            }
        },
        methods: {
            showDelete() {
                this.isDeleteVisible = true
            },
            hideDelete() {
                this.isDeleteVisible = false
            }
        },
        computed: {
            modeCompleted() {
                if (this.darkMode && this.todo.isCompleted) {
                    return 'darkCompleted'
                } else if (!this.darkMode && this.todo.isCompleted) {
                    return 'lightCompleted'
                } else if (this.darkMode && !this.todo.isCompleted) {
                    return 'darkNotCompleted'
                } else {
                    return 'lightNotCompleted'
                }
            }
        },
        emits: ['toggleTodoComplete', 'deleteTodo']
    }
</script>


<style scoped>
    .todo {
        width: 100%;
        display: grid;
        grid-template-columns: 50px auto 50px;
        align-items: center;
        border-bottom: hsl(236, 9%, 61%) 1px solid;
        padding: 20px;
        color: hsl(233, 11%, 84%); 
        cursor: pointer;
    }

    p {
        justify-self: flex-start;
    }

    .btn-delete img {
        border-radius: 50%;
    }

    .btn-delete {
        justify-self: flex-end;
        border: none;
        background-color: transparent;
    }

    .lightCompleted {
        text-decoration: line-through;
        color: hsl(236, 9%, 61%);
    }

    .darkCompleted {
        text-decoration: line-through;
        color: hsl(234, 11%, 52%);
    }

    .lightNotCompleted {
        color: hsl(235, 19%, 35%);
    }

    .darkNotCompleted {
        color: hsl(234, 39%, 85%);
    }
</style>