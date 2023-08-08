<template>
  <div class="app"
  :style="{backgroundColor: darkMode ? 'hsl(235, 21%, 11%)' : 'hsl(0, 0%, 98%)'}">
  
      <img :src="currentBg" class="bg-img"/>
      <MainSection :darkMode="darkMode" @toggleMode="toggleMode"/>
    
  </div>
</template>

<script>
  import MainSection from './components/MainSection';

export default {
  name: 'App',
  components: {
    MainSection
  }, 
  data() {
    return {
      darkMode: true,
      windowWidth: window.innerWidth
    }
  },
  methods: {
    toggleMode() {
      this.darkMode = !this.darkMode
    },

    onWindowResize() {
      this.windowWidth = window.innerWidth
    }
  },

  computed: {
    currentBg() {
      if(this.windowWidth > 1024) {
        if (this.darkMode) {
          return require('./assets/images/bg-desktop-dark.jpg')
        } else {
          return require('./assets/images/bg-desktop-light.jpg')
        }
      } else {
        if (this.darkMode) {
          return require('./assets/images/bg-mobile-dark.jpg')
        } else {
          return require('./assets/images/bg-mobile-light.jpg')
        }
      }
    }
  },

  mounted() {
    window.addEventListener('resize', this.onWindowResize)
  },

  beforeUnmount() {
    window.removeEventListener('resize', this.onWindowResize)
  },
}
</script>


<style>
  @import './style.css';

  .app {
    min-height: 100vh;
    display: grid;
  }

  .bg-img {
    width: 100%;
    grid-area: 1 / 1 / 2 / 2;
    z-index: 1;
  }

</style>
