<template>
  <v-app id="app">
    <v-navigation-drawer
      fixed
      :clipped="$vuetify.breakpoint.mdAndUp"
      app
      v-model="drawer"
      v-if="logueado"
    >     
     
    </v-navigation-drawer>

    <v-app-bar
      :clipped-left="$vuetify.breakpoint.lgAndUp"
      app
      color="blue darken-3"
      dark
    >
    
      <v-toolbar-title
        style="width: 300px"
        class="ml-0 pl-3"
      >
        <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>
        <span class="hidden-sm-and-down">Faceboot</span>
      </v-toolbar-title>
      <v-text-field
        flat
        solo-inverted
        hide-details
        prepend-inner-icon="search"
        label="Search"
        class="hidden-sm-and-down"
      ></v-text-field>
      <v-spacer></v-spacer>

      <v-btn text @click="salir()" v-if="logueado">
        <v-icon>logout</v-icon> Salir
      </v-btn>
      <v-btn to="/login" text v-if="['register'].includes($route.name)">
      Login
      </v-btn>
      <v-btn to="/register" text v-if="['login'].includes($route.name)">
      Registro
      </v-btn>
    </v-app-bar>
    
    <v-content>
      <v-container
        fluid
      >
        <v-slide-y-transition mode="out-in">
          <router-view/>
        </v-slide-y-transition>
      </v-container>
    </v-content>
  </v-app>
</template>
 
<script>
import HelloWorld from './components/HelloWorld';
export default {
  
  name: 'App',
  data () {
    return {
      drawer: true,
      links: [
        { icon: 'home', text: 'Home', route: '/'},
        { icon: 'contacts', text: 'About', route: '/about'},
      ]
    }
    
  },
  computed:{
    logueado(){
      return this.$store.state.usuario;
    },
    esUsuario(){
      return this.$store.state.usuario && this.$store.state.usuario.rol.id == 'usuario';
    }
  },
  created(){
    this.$store.dispatch("autoLogin");
  },
  methods:{
    salir(){
      this.$store.dispatch("salir");
    }
  }
}
</script>
