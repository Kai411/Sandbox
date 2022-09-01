<template>
  <v-container class="ma-0 pa-0" fluid style="position: relative">
    <v-menu
      v-model="menu"
      :close-on-content-click="false"
      left
      offset-x
      style="position: fixed"
    >
      <template v-slot:activator="{ on, attrs }">
        <v-btn
          :ripple="false"
          class="btn item-hover mt-2"
          text
          color="#34eb55"
          dark
          v-bind="attrs"
          v-on="on"
          style="position: fixed; right: 1%; z-index: 10000"
        >
          <v-icon size="30">mdi-playlist-play</v-icon>
        </v-btn>
      </template>

      <v-card
        style="background: #3c414a; border-radius: 8px"
        elevation="0"
        class="pt-2 px-3 d-flex flex-column menu-card"
      >
        <v-btn
          class="show-playing"
          color="#34eb55"
          :ripple="false"
          :loading="bgmLoading"
        >
          <v-icon>mdi-play</v-icon
          >{{ $vuetify.breakpoint.xs ? 'Now - ' : 'Playing Now - ' }}
          <marquee
            class="ml-1 mr-1 my-auto"
            :width="$vuetify.breakpoint.xs ? '40%' : '25%'"
            direction="right"
            scrollamount="3"
            >{{ playing }}</marquee
          >
        </v-btn>
        <div class="player">
          <v-btn
            v-for="(music, index) in musics"
            :key="index"
            color="white"
            outlined
            style="width: 100%"
            class="mt-1"
            @click="change(music.name, music.src)"
            >{{ music.name }}</v-btn
          >
        </div>

        <v-slider
          dense
          class="mt-4 mb-0 pb-0"
          v-model="volume"
          :min="min"
          :max="max"
          step="0.01"
          color="#34eb55"
          track-color="#606c82"
          ><v-icon
            class="item-hover"
            slot="prepend"
            color="#34eb55"
            @click="muted ? unmute() : mute()"
            >{{ muted ? 'mdi-volume-mute' : 'mdi-volume-high' }}</v-icon
          ></v-slider
        >
      </v-card>
    </v-menu>

    <v-btn
      color="#34eb55"
      class="mute-btn pl-0"
      style="right: 4.5%"
      text
      @click="menu = true"
    >
      <span>Now Playing - </span
      ><marquee
        class="ml-1"
        :width="$vuetify.breakpoint.xs ? '30%' : '55%'"
        direction="right"
        :style="
          $vuetify.breakpoint.xs ? 'margin-right: 0px' : 'margin-right: -15px'
        "
        scrollamount="3"
        >{{ this.playing }}</marquee
      ></v-btn
    ><v-btn
      :ripple="false"
      color="#fff"
      text
      @click="muted ? unmute() : mute()"
      class="btn mute-btn item-hover px-0"
      style="mix-blend-mode: difference"
    >
      <span
        ><v-icon size="30">{{
          !muted ? 'mdi-volume-mute' : 'mdi-volume-high'
        }}</v-icon></span
      >
    </v-btn>

    <v-btn
      :ripple="false"
      text
      style="
        position: fixed;
        z-index: 10000;
        color: white;
        mix-blend-mode: difference;
      "
      class="mt-2 btn item-hover"
      @click="
        () => {
          this.$router.push('/')
        }
      "
      ><v-icon>mdi-chevron-left</v-icon>Back</v-btn
    >

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
        <span class="ma-auto">Hello.</span
        ><v-btn
          href="#2"
          class="btn chevron-btn item-hover"
          :ripple="false"
          text
          style="color: #fff"
          ><v-icon :size="$vuetify.breakpoint.xs ? '60' : '70'"
            >mdi-chevron-down</v-icon
          >
        </v-btn>
      </h1>
    </section>
    <div
      id="2"
      class="d-flex"
      style="background: white; height: 100vh; padding: 100px"
    >
      <video
        id="bgm1"
        ref="bgm"
        :src="src"
        loop
        style="display: none"
        controls
        type="video/mp4"
      ></video>

      <h1 style="color: black">test</h1>
    </div>
    <div class="" style="background: black; height: 100vh; padding: 100px">
      <h1 style="color: white">4</h1>
    </div>
  </v-container>
</template>

<script>
import Vue from 'vue'

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
// import lottie from 'vue-lottie/src/lottie.vue'
// import * as hi from '~/assets/hi.json'

import VideoPlayer from 'nuxt-video-player'
// require('nuxt-video-player/src/assets/css/main.css')
import Suzume from '../assets/Suzume.mp4'
import tenkiBgm from '../assets/Tenki.mp4'
import suzumeBgm from '../assets/SuzumeBgm.mp4'
import kiminawaBgm from '../assets/kiminawaBgm.mp4'

export default {
  name: 'LearnPage',
  data() {
    return {
      image: '',
      option: '',
      imgLoading: false,
      Suzume,
      tenkiBgm,
      suzumeBgm,
      src: suzumeBgm,
      muted: false,
      min: 0,
      max: 0.5,
      volume: 0.2,
      prevVolume: null,
      playing: null,
      menu: false,
      bgmLoading: false,
      musics: [
        {
          name: 'Suzume no Tojimari',
          src: suzumeBgm,
        },
        {
          name: 'Sky is Clearing Up',
          src: tenkiBgm,
        },
        {
          name: 'Kataware Doki',
          src: kiminawaBgm,
        },
      ],

      // lottieOptions: {
      //   animationData: hi.default,
      //   loop: false,
      // },
      // anim: null, // for saving the reference to the animation
    }
  },
  components: {
    // lottie,
    VideoPlayer,
  },
  methods: {
    mute() {
      var video = document.getElementById('bgm1')
      this.prevVolume = this.volume
      this.volume = 0
      video.volume = this.volume
      this.muted = true
    },
    unmute() {
      var video = document.getElementById('bgm1')
      this.volume = this.prevVolume
      video.volume = this.volume
      this.muted = false
    },
    change(name, src) {
      this.$refs.bgm.pause()
      this.src = src
      this.playing = name
      var video = document.getElementById('bgm1')
      video.volume = this.volume
      this.muted = false
      console.log('wait')
      this.bgmLoading = true
      setTimeout(() => {
        this.play()
      }, 2000)
    },
    play() {
      console.log('play')
      this.$refs.bgm.play()
      this.bgmLoading = false
    },
  },
  mounted() {
    // this.$refs.videoPlayer.play()
    // if (this.$vuetify.breakpoint.xs) {
    //   window.scrollTo(0, 1)
    // }
    // let xs = this.$vuetify.breakpoint.xs
    // if (xs) {
    //   window.scrollTo(0, 1)
    // }
    document.body.requestFullscreen()
    console.log(this.$vuetify.breakpoint.xs)

    let random = Math.floor(Math.random() * 3)
    this.playing = this.musics[random].name
    this.src = this.musics[random].src
    setTimeout(() => {
      this.play()
    }, 1000)
    this.$refs.suzume.play()

    var video = document.getElementById('bgm1')
    video.volume = this.volume
  },
  watch: {
    volume(volume) {
      var video = document.getElementById('bgm1')
      video.volume = volume
      if (volume === 0) {
        this.muted = true
      } else {
        this.muted = false
      }
    },
  },
}
</script>

<style>
.btn:hover {
  transform: scale(1.2);
}
.vidSection {
  height: 100vh;
  width: 100%;
  position: relative;
}
video {
  height: 100%;
  width: 100%;
  object-fit: cover;
  position: absolute;
}
.suzume {
  width: 100%;
  height: 100%;
  background-color: #000;
  font-size: calc(100vh / 1.8);
  font-weight: bold;
  color: #fff;
  mix-blend-mode: multiply;
}
.chevron-btn {
  position: absolute;
  left: 50%;
  bottom: 10%;
  transform: translate(-50%, -50%);
  z-index: 10000;
  color: #fff;
}
.menu-card {
  width: 270px;
}
@media (max-width: 480px) {
  .suzume {
    font-size: 100px;
    mix-blend-mode: plus-lighter;
  }
  .chevron-btn {
    left: 50%;
    bottom: 12%;
  }
  .menu-card {
    width: 220px;
  }
}
.btn::before {
  background-color: transparent !important;
}
.btn:hover {
  transform: scale(1.2);
}
.suzumeBg {
  filter: saturate(1.8);
}
.mute-btn {
  position: fixed;
  z-index: 10000;
  right: 1%;
  bottom: 3%;
}
.player {
  overflow: overlay;
  overflow-y: scroll;
  height: 100px;
  -ms-overflow-style: none;
  scrollbar-width: none;
  -moz-box-shadow: inset 0 0 10px #000000;
  -webkit-box-shadow: inset 0 0 10px #000000;
  box-shadow: inset 0 -7px 9px -7px rgba(52, 235, 85, 0.2);
}
.player::-webkit-scrollbar-thumb {
  background-color: transparent;
  border: 6px solid transparent;
  background-clip: content-box;
}
.player::-webkit-scrollbar {
  display: none;
}
.show-playing {
  filter: drop-shadow(0px 10px 20px rgb(52, 235, 85, 0.2));
}
</style>
