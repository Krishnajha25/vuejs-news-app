<template>
  <v-app>
    <div>
      <Navigation />
      <v-main>
        <router-view></router-view>
      </v-main>
    </div>  
  </v-app>
  
</template>

<script>
import Navigation from './components/Navigation'

export default {
  name: 'App',

  components: {
    Navigation
  },

  data: () => ({
    //
  }),
};
</script>
