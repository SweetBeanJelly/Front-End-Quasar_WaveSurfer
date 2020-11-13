<template>
  <q-layout view="lHh Lpr lFf">
    <q-header class="bg-white text-black">
      <q-toolbar>

        <q-toolbar-title>
          Quasar + WaveSurfer Audio Player
        </q-toolbar-title>

        <q-btn color="red" text-color="white">
        File Load
        <input
            type="file"
            class="q-uploader__input overflow-hidden absolute-full"
            v-on:change="fileChosen"
            ref="fileInput"
            accept="audio/mpeg"
        />
        </q-btn>

      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
      content-class="bg-transparent"
    >
      <q-list>
        <q-item-label
          header
          class="text-transparent"
        >
          Essential Links
        </q-item-label>
        <EssentialLink
          v-for="link in essentialLinks"
          :key="link.title"
          v-bind="link"
        />
      </q-list>
    </q-drawer>

    <q-page-container class="audio-container">
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import EssentialLink from 'quasar'
import { EventBus } from "../services/event-bus.js";

export default {
  name: 'MainLayout',
  components: { EssentialLink },
  data () {
    return {
      leftDrawerOpen: false,
      essentialLinks: linksData
    }
  },
  methods: {
    fileChosen(file) {
        EventBus.$emit("fileChosen", file);
    }    
  }
}
</script>

<style>
.audio-container {
  position: absolute;
  top: 0;
  left: 0;
  height: 100%;
  width: 100%;
  background: linear-gradient(rgba(0, 0, 0, 0.3), rgba(0, 0, 0, 0.3)),
    url("../assets/audio.jpg") no-repeat center;
  background-size: cover;
}
</style>
