<template>
  <img width="200" v-for="(img, idx) in images" :src="img" @click="openGallery(idx)" />
  <VGaller v-model="show" :images="images" :index="index" />
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'
import VGaller from './components'

export default defineComponent({
  name: 'App',

  components: {
    VGaller
  },

  setup() {
    const show = ref(false)
    const index = ref(0)
    const images = [
      "https://images.unsplash.com/photo-1618217483504-1fd1966e2a4f?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1900&q=80",
      "https://images.unsplash.com/photo-1618199901175-5e026466a6cb?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1534&q=80",
      "https://images.unsplash.com/photo-1618204948550-3b60d5668b13?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1534&q=80",
      "https://images.unsplash.com/photo-1618220244721-241b3c831a00?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=3304&q=80",
      'https://cdn.pixabay.com/photo/2015/09/02/13/19/ocean-918999_1280.jpg'
    ];

    const openGallery = (idx: number) => {
      index.value = idx
      show.value = true
    }

    return { show, images, index, openGallery }
  }
})
</script>

<style>
html,
body {
  margin: 0;
  padding: 0;
}

img {
  cursor: pointer;
}
</style>
