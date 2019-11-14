<template>
  <div>
    <div class="app-main-layout">
      <navbar @clicked="isOpen=!isOpen"/>
      <sidebar v-model="isOpen"/>
      <main class="app-content" :class="{full: !isOpen}">
        <div class="app-page">
          <router-view/>
        </div>
      </main>
      <div class="fixed-action-btn">
        <router-link class="btn-floating btn-large blue" to="/record">
          <i class="large material-icons">add</i>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import Sidebar from '../components/Bars/Sidebar'
import Navbar from '../components/Bars/Navbar'

export default {
  name: 'main-layout',
  data: () => ({
    isOpen: false
  }),
  components: {
    Sidebar,
    Navbar
  }
}
</script>
