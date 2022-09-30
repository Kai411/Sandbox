<template>
  <v-container class="ma-0 pa-0" fluid>
    <section style="height: 102vh">
      <div class="" style="background-color: black; height: 100%">
        <v-row
          ><v-col style="flex-grow: 0"
            ><lottie
              :width="200"
              :height="200"
              :options="lottieOptions" /></v-col
        ></v-row>

        <v-row
          ><v-col class="pa-16"
            ><p class="item-hover">
              <span style="color: white"
                >Lorem, ipsum dolor sit amet consectetur adipisicing elit.
                Dolor, ipsam. Maiores, est alias? Est nemo beatae similique
                consequatur eligendi in, delectus assumenda maxime tempora quo
                debitis ipsam recusandae nobis sunt?</span
              >
            </p>

            <v-btn
              class="btn item-hover d-flex"
              outlined
              color="white"
              @click="$router.push('/isekai')"
              >Isekai 💥
            </v-btn>
          </v-col></v-row
        >
      </div>
    </section>

    <div class="" style="height: 100vh; background: white">
      <v-btn outlined color="black">Test</v-btn>
    </div>
    <div class="" style="height: 100vh; background: black">
      <section class="vidSection">
        <video
          class="suzumeBg"
          ref="suzume"
          :src="Suzume"
          muted
          loop
          style="height: 100vh"
        ></video>

        <h1 class="suzume d-flex flex-column">
          <span class="mt-10">Hi</span>
          <span class="">Test</span>
          <span class="">Idk</span>
          <!-- <v-btn
            href="#2"
            class="chevron-btn item-hover"
            :ripple="false"
            text
            style="color: #fff"
            ><v-icon :size="$vuetify.breakpoint.xs ? '60' : '70'"
              >mdi-chevron-down</v-icon
            >
          </v-btn> -->
        </h1>
      </section>
    </div>
  </v-container>
</template>

<script>
import Vue from 'vue'
import megumin from '../assets/Megumin.png'
Vue.directive('hover-direction', {
  inserted(el) {
    el.addEventListener('mousemove', ({ offsetX }) => {
      let side = offsetX > el.clientWidth / 2 ? 'right' : 'left'
      if (!el.classList.contains('left') && !el.classList.contains('right'))
        el.classList.add(side)
    })

    el.addEventListener('mouseleave', () => {
      el.classList.remove('left')
      el.classList.remove('right')
    })
  },
})
import lottie from 'vue-lottie/src/lottie.vue'
import * as hi from '~/assets/hi.json'

import Suzume from '../assets/Suzume.mp4'

export default {
  name: 'IndexPage',
  data() {
    return {
      image: '',
      option: '',
      imgLoading: false,
      megumin,
      Suzume,
      lottieOptions: {
        animationData: hi.default,
        loop: false,
      },
      anim: null, // for saving the reference to the animation
    }
  },
  components: {
    lottie,
  },
  methods: {
    //
  },
  mounted() {
    this.$refs.suzume.play()
  },
}
</script>

<style>
.btn:hover {
  transform: scale(1.2);
}
.suzume {
  width: 100%;
  height: 100%;
  background-color: #000;
  /* font-size: calc(100vh / 1.8); */
  font-weight: bold;
  color: #fff;
  mix-blend-mode: multiply;
  position: relative;
}
</style>
