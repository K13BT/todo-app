<template>
    <div class="container">
      <HeaderMode @toggle-mode="$emit('toggleMode')" :darkMode="darkMode"/>

      <NewTodo @createNewTodo="createNewTodo" :darkMode="darkMode" />

      <div class="todos"  :style="{backgroundColor: darkMode ? 'hsl(235, 24%, 19%)' : 'hsl(0, 0%, 98%)', boxShadow: darkMode ? '0 10px 10px #111' : '0 10px 10px hsl(233, 11%, 84%)'}">
        <TodoList :todos="currentTodos" @deleteTodo="deleteTodo" @toggleTodoComplete="toggleTodoComplete" :darkMode="darkMode"  v-if="todos.length !== 0" @onDrag="onDrag"/>

        <NoTodos v-else :darkMode="darkMode"/>
        
      </div>

      <MenuBar 
        :darkMode="darkMode"
        @activeClick="activeClick" @allClick="allClick" @completedClick="completedClick"
        @clearCompleted="clearCompleted"
        :itemsLeft="(todos.filter(todo => !todo.isCompleted)).length"
        :completed="completed" :active="active"/>

      <p class="footer">Drag and drop to reorder list</p>
    </div>
</template>


<script>
    import NoTodos from './NoTodos'
    import NewTodo from './NewTodo'
    import MenuBar from './MenuBar'
    import TodoList from './TodoList'
    import HeaderMode from './HeaderMode'
    export default {
        name: 'MainSection',
        components: {
        NewTodo,
        MenuBar,
        TodoList,
        HeaderMode,
        NoTodos
    },
    props: {
        darkMode: Boolean,
    },
    emits: [
        'toggleMode'
    ],
        
    data() {
        return {
        todos: [],
        active: false,
        completed: false
        }
    },
    
  methods: {
    createNewTodo(newTodo) {
      this.todos = [...this.todos, newTodo]
    }, 

    deleteTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id)
    },

    // Marks todo completed
    toggleTodoComplete(id) {
      this.todos = this.todos.map(todo => {
        if(todo.id === id) {
          return {...todo, isCompleted: !todo.isCompleted}
        }
        return todo
      })
    },

    activeClick() {
      this.active = true 
      this.completed = false
    },

    allClick() {
      this.active = false 
      this.completed = false
    },

    completedClick() {
      this.active = false 
      this.completed = true
    },

    clearCompleted() {
      this.todos = this.todos.filter(todo => !todo.isCompleted)
    },
    onDrag(reorderedTodos) {
        this.todos = reorderedTodos
    }
  },
    computed: {
        currentTodos() {
        if (this.active) {
            return this.todos.filter(todo => !todo.isCompleted)
        } else if (this.completed) {
            return this.todos.filter(todo => todo.isCompleted)
        } else {
            return this.todos
        }
        }
    }
    }
</script>


<style>
  .container {
    width: 700px;
    margin: 80px auto;
    grid-area: 1 / 1 / 2 / 2;
    z-index: 2;
  }

  .todos {
    border-top-left-radius: 5px;
    border-top-right-radius: 5px;
  }

  .footer {
    text-align: center;
    margin-top: 50px;
    color: hsl(234, 11%, 52%);
  }

  @media (max-width: 1024px) {
    .container {
      width: 500px;
    }
  }

  @media (max-width: 768px) {
    .container {
      width: 400px;
    }
  }

  @media (max-width: 525px) {
    .container {
      width: 300px;
    }
  }
</style>