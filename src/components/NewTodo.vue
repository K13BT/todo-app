<template>
    <form @submit="onSubmit" :style="{backgroundColor: darkMode ? 'hsl(235, 24%, 19%)' : 'hsl(0, 0%, 98%)'}" :class="{'form-light' : !darkMode}">
        <button :class="isCompleted ? 'completed-check' : 'checkbox'" @click="onButtonClick" type="button">
            <img v-show="isCompleted" src="../assets/images/icon-check.svg" />
        </button>
        <input type="text" v-model="text" name="todo" placeholder="Create a new todo..." 
        :style="{ boxShadow: darkMode ? 'inset 0 0 30px 30px hsl(235, 24%, 19%)' : 'inset 0 0 30px 30px #fff' ,
        color: darkMode ? 'hsl(234, 39%, 85%)' : 'hsl(235, 19%, 35%)' }"/>
    </form>
</template>

<script>
export default {
    name: 'NewTodo',
    props: {
        darkMode: Boolean
    },
    data() {
        return {
            text: '',
            isCompleted: false
        }
    },
    emits: ["createNewTodo"],

    methods: {
        onSubmit(e) {
            e.preventDefault()
            if(this.text === '') {
                return
            }
            const newTodo = {
                id: Math.floor(Math.random() * 10000000),
                text: this.text,
                isCompleted: this.isCompleted
            }
       
            this.$emit('createNewTodo', newTodo)
            this.text = ''
            this.isCompleted = false
        },
        onButtonClick() {
            this.isCompleted = !this.isCompleted
        }
    }
}
</script>


<style scoped> 
    input {   
        border: none;
        background-color: transparent;
        font-size: 18px;
        color: hsl(236, 9%, 61%);
    }

    input:focus {
        outline: none;
    }

    form {
        margin-bottom: 30px;
        padding: 20px;
        border-radius: 5px;
        display: flex;
        align-items: center; 
    }


    @media (max-width: 525px) {
        input {
            font-size: 15px;
        }
    }

    @media (max-width: 398px) {
        .form-light {
            box-shadow: 0 10px 10px hsl(233, 11%, 84%);
        }
    }
</style>