<template>
  <v-app>
    <!-- <v-app-bar fixed app>
      <v-toolbar-title v-text="title" />
      <v-spacer />
    </v-app-bar> -->
    <v-main>
      <v-container fluid class="ma-0 pa-0">
        <Nuxt />
        <VueCursor scaleElement="item-hover" :cursorColor="'#fff'" />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import VueCursor from '../components/Vcursor.vue'

export default {
  name: 'DefaultLayout',
  data() {
    return {
      //
    }
  },
  components: {
    VueCursor,
  },
}
</script>

<style>
html {
  overflow: overlay;
  overflow-x: hidden;
  scroll-behavior: smooth;
}
/* * {
  cursor: none !important;
} */
::-webkit-scrollbar {
  width: 20px;
}

::-webkit-scrollbar-track {
  background: transparent;
}

::-webkit-scrollbar-thumb {
  background-color: #d6dee1;
  border-radius: 20px;
  border: 6px solid transparent;
  background-clip: content-box;
}

::-webkit-scrollbar-thumb:hover {
  background-color: #8ca5ae;
}
</style>
