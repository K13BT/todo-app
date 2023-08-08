<template>
    <div class="menu-bar"
    :style="{backgroundColor: darkMode ? 'hsl(235, 24%, 19%)' : 'hsl(0, 0%, 98%)', boxShadow: darkMode ? '0 10px 10px #111' : '0 10px 10px hsl(233, 11%, 84%)'}">
        <p>{{ itemsLeft }} items left</p>
                
        <menu>
            <li>
                <button @click="$emit('allClick')" :style="all && 'color : hsl(220, 98%, 61%)'" :class="darkMode ? 'dark-hover' : 'light-hover'">All</button>
            </li>
            <li>
                <button @click="$emit('activeClick')" :style="active && 'color : hsl(220, 98%, 61%)'" :class="darkMode ? 'dark-hover' : 'light-hover'">Active</button>
            </li>
            <li>
                <button @click="$emit('completedClick')"  :style="completed && 'color : hsl(220, 98%, 61%)'" :class="darkMode ? 'dark-hover' : 'light-hover'">Completed</button>
            </li>
        </menu>

        <button @click="$emit('clearCompleted')" class="clear-completed" :class="darkMode ? 'dark-hover' : 'light-hover'">Clear Completed</button>

    </div>

    <!-- Menubar Mobile -->
    <div class="menu-bar-mobile">
    <div :style="{backgroundColor: darkMode ? 'hsl(235, 24%, 19%)' : 'hsl(0, 0%, 98%)', boxShadow: darkMode ? '0 10px 10px #111' : '0 10px 10px hsl(233, 11%, 84%)'}" class="items-clear">
        <p>{{ itemsLeft }} items left</p>
    
        <button @click="$emit('clearCompleted')" class="clear-completed" :class="darkMode ? 'dark-hover' : 'light-hover'">Clear Completed</button>
    </div>

    <menu :style="{backgroundColor: darkMode ? 'hsl(235, 24%, 19%)' : 'hsl(0, 0%, 98%)', boxShadow: darkMode ? '0 10px 10px #111' : '0 10px 10px hsl(233, 11%, 84%)'}">
        <li>
            <button @click="$emit('allClick')" :style="all && 'color : hsl(220, 98%, 61%)'" :class="darkMode ? 'dark-hover' : 'light-hover'">All</button>
        </li>
        <li>
            <button @click="$emit('activeClick')" :style="active && 'color : hsl(220, 98%, 61%)'" :class="darkMode ? 'dark-hover' : 'light-hover'">Active</button>
        </li>
        <li>
            <button @click="$emit('completedClick')"  :style="completed && 'color : hsl(220, 98%, 61%)'" :class="darkMode ? 'dark-hover' : 'light-hover'">Completed</button>
        </li>
    </menu>

    </div>
</template>


<script>
export default {
    name: 'MenuBar',
    props: {
        itemsLeft: Number,
        completed: Boolean,
        active: Boolean,
        darkMode: Boolean
    },
    emits: ['allClick', 'activeClick', 'completedClick', 'clearCompleted'],
    computed: {
        all() {
            if (!this.active && !this.completed) {
                return true
            } else {
                return false
            }
        }
    }
}
</script>


<style scoped> 
    .menu-bar {
        color: hsl(234, 11%, 52%);
        display: grid;
        grid-template-columns: repeat(3, 1fr);
        justify-content: space-between;
        align-items: center;
        font-weight: bold;
        padding: 25px;
        border-bottom-left-radius: 5px;
        border-bottom-right-radius: 5px;
    }

    menu {
        display: flex;
        justify-content: center;
    }
    
    li {
        list-style-type: none;
        margin-right: 20px;
    }

    p {
        justify-self: flex-start;
        color: hsl(234, 11%, 52%);
    }

    .clear-completed {
        justify-self: flex-end;
    }

    button {
        background-color: transparent;
        border: none;
        color: hsl(234, 11%, 52%);
        font-weight: bold;
    } 

    .menu-bar-mobile {
        display: none;
    }

    .light-hover:hover {
        color: hsl(235, 19%, 35%);
    }

    .dark-hover:hover {
        color: hsl(236, 33%, 92%);
    }
    
    @media(max-width: 1024px) {
        .menu-bar-mobile {
            display: grid;
        }

        .items-clear {
            display: flex;
            justify-content: space-between;
            margin-bottom: 20px;
            border-bottom-left-radius: 5px;
            border-bottom-right-radius: 5px;
            padding: 20px;
            
        }

        menu {
            padding: 20px;
            border-radius: 5px;
        }

        .menu-bar {
            display: none;
        }
    }
</style>