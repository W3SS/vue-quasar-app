<template>
  <q-layout ref="layout" view="hHr LpR Fff">
    <q-toolbar slot="header" class="toolbar">
      <q-btn flat @click="$refs.layout.toggleLeft()">
        <q-icon name="menu"></q-icon>
      </q-btn>
      <div class="q-toolbar-title">
        VIP VR360
      </div>
    </q-toolbar>
    
    <div slot="left">
      <q-item-main id="menu-header" label="Menu"></q-item-main>
      <q-side-link item to="/" exact>
        <q-icon name="home"></q-icon>
        <q-item-main label="Home"></q-item-main>
      </q-side-link>
      <q-side-link item to="/streaming" exact>
        <q-icon name="cloud_circle"></q-icon>
        <q-item-main label="Streaming Videos"></q-item-main>
      </q-side-link>
      <q-side-link item to="/360RobotDemo" exact>
        <q-icon name="ondemand_video"></q-icon>
        <q-item-main label="Behind the Scenes"></q-item-main>
      </q-side-link>
      <q-side-link item to="/about" exact>
        <q-icon name="info"></q-icon>
        <q-item-main label="About"></q-item-main>
      </q-side-link>
    </div>
    <div id="homebackground" class="layout-view">
      <div class="columns">
        <div class="column" style="padding:0px;">
          <div class="top-banner has-text-centered">
            <img src="~assets/bannerclear.png" style="max-height:none; width:auto; height:auto; max-width:75%; display:block; margin: 0 auto;">
          </div>
        </div>  
      </div>
      <q-transition
        appear
        group
        enter="fadeIn"
        leave="fadeOut"
      >
      <div v-for="video in this.$store.state.videos" v-bind:key="video"  class="columns">
        <div class="column">
          <router-link to="/video">
            <div class="card" @click="setSrc(video)">
              <a class="">
                <img :src="video.thumbnail">
              </a>
              <p>{{ video.label }}</p>
            </div>
          </router-link>
        </div>
      </div> 
    </q-transition>
      <q-btn
        v-back-to-top.animate="{offset: 500, duration: 200}"
        round
        color="dark"
        class="fixed-bottom-right animate-pop"
        style="margin: 0 15px 15px 0"
      >
        <q-icon name="keyboard_arrow_up"></q-icon>
      </q-btn>
    </div>
  </q-layout>
</template>

<script>
import { QLayout, QToolbar, QSideLink, QIcon, QItemMain, QBtn, BackToTop, QTransition } from 'quasar'
import 'quasar-extras/animate/fadeIn.css'
import 'quasar-extras/animate/fadeOut.css'
export default {
  data () {
    return {
      search: ''
    }
  },
  components: {
    QLayout,
    QToolbar,
    QSideLink,
    QIcon,
    QItemMain,
    QBtn,
    QTransition
  },
  directives: {
    BackToTop
  },
  mounted () {
    screen.orientation.lock('portrait')
  },
  methods: {
    setSrc: function (video) {
      this.$store.state.videoSrc = video.source
    }
  }
}
</script>
<style scoped lang="scss">

#homebackground {
  background: linear-gradient(to top, #2b2e35, #2d3540);
  padding-top: 10px;
  overflow-x: hidden;
  padding-bottom: 75px;
}

.card {
  background-color: rgba(100, 100, 100, 0.1);
  box-shadow: 0 14px 28px rgba(0, 0, 0, 0.25), 0 10px 10px rgba(0, 0, 0, 0.22);
  margin: auto;
  width: 90%;
  max-width: 320px;
  display: block;
  padding-top: 10px;
  padding: 12px;

  img {
    width: 100%;
    max-width: 286px;
    margin-left: 2.5%;
    margin-bottom: 10px;
    border-radius: 4px;
    display: block;
    margin: auto;
  }

  p {
    text-align: center;
    margin-bottom: 1px;
    color: white;
  }
}

.top-banner {
  background-color: rgba(0, 0, 0, 0.2);
  padding: 10px;
  margin-bottom: 10px;
  color: white;
  p {
    margin-top: 10px;
  }
}
</style>
