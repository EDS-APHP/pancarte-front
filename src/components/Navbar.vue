<template>
<b-navbar toggleable='md' type='dark' variant='dark'>

  <b-navbar-toggle target='nav_collapse'></b-navbar-toggle>


  <b-collapse is-nav id='nav_collapse'>

    <b-navbar-nav>
      <b-nav-item><router-link style='color:white' to='/'>Accueil</router-link></b-nav-item>
      <b-nav-item><router-link style='color:white' to='/rooms'>Vue générale</router-link></b-nav-item>
    </b-navbar-nav>
  </b-collapse>

  <b-navbar-brand class='ml-auto mt-3'><h2><b>{{msg}}</b></h2></b-navbar-brand>
  <b-navbar-brand class='ml-auto mt-3'>{{datenow}}</b-navbar-brand>

    <!-- Right aligned nav items -->
    <b-collapse is-nav id='nav_collapse'>
    <b-navbar-nav class='ml-auto'>

      <b-nav-item-dropdown text='Langue' right>
        <b-dropdown-item href='#'>EN</b-dropdown-item>
        <b-dropdown-item href='#'>ES</b-dropdown-item>
        <b-dropdown-item href='#'>RU</b-dropdown-item>
        <b-dropdown-item href='#'>FA</b-dropdown-item>
      </b-nav-item-dropdown>

      <b-nav-item-dropdown right>
        <!-- Using button-content slot -->
        <template slot='button-content'>
          <em>{{User}}</em>
        </template>
        <b-dropdown-item href='#'>Profil</b-dropdown-item>
        <b-dropdown-item href='#'>Déconnexion</b-dropdown-item>
      </b-nav-item-dropdown>
    </b-navbar-nav>

  </b-collapse>
</b-navbar>
</template>

<script>
import moment from 'moment'
moment.locale('fr')

export default {
  name: 'Navbar',
  data () {
    return {
      msg: 'Pancarte Front',
      datenow: '',
      User: 'Jonas Pochard'
    }
  },
  methods: {
    time () {
      var self = this
      this.datenow = moment().format('D MMMM YYYY H:mm:ss')
      setTimeout(self.time, 1000)
    }
  },
  mounted: function () {
    this.time()
  }
}
</script>

<style scoped>
</style>

