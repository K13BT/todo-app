<template>
        <draggable :list="localTodos" class="dragArea list-group sortable-chosen" @end="handleDragEnd" @start="handDragStart">
        <div v-for="(todo, index) in todos" 
        :key="index" :class="{'dragged-item' : index === draggedItemIndex}">

            <SingleTodo :todo="todo" 
            @deleteTodo="$emit('deleteTodo', todo.id)" @toggleTodoComplete="$emit('toggleTodoComplete', todo.id)" :darkMode="darkMode"/>

        </div>
        </draggable>
</template>


<script>
    import SingleTodo from './SingleTodo'
    import {VueDraggableNext} from 'vue-draggable-next'

    export default {
        name: 'TodoList',
        components: {
            SingleTodo,
            draggable: VueDraggableNext
        },
        props: {
            todos: Array,
            darkMode: Boolean
        }, 
        data() {
            return {
                localTodos: [...this.todos],
                draggedItemIndex: null
            }
        },
        emits: ['deleteTodo', 'toggleTodoComplete', 'onDrag'],
        methods: {
            handleDragEnd() {
                this.draggedItemIndex = null
                this.$emit('onDrag', this.localTodos);
            },
            handDragStart(e) {
                this.draggedItemIndex = e.oldIndex
            }
        },
        watch: {
            todos: {
                handler(newValue) {
                    this.localTodos = [...newValue]
                },
                immediate: true
            }
        }
    }
</script>


<style scoped>
    .sortable-chosen {
        transition: all 0.3s ease;
    }

    .dragged-item {
        background-color: hsl(237, 14%, 26%);
        scale: 1.03;
    }
</style>