<template>
  <button @click="showGallery = true">Open</button>
  <VGallery v-model:show="showGallery" :images="images" :index="0" />
</template>

<script>
import { defineComponent, ref } from "vue";
import VGallery from './index'

export default defineComponent({
  components: {
    VGallery
  },

  setup() {
    const images = [
      "https://images.unsplash.com/photo-1618217483504-1fd1966e2a4f?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1900&q=80",
      "https://images.unsplash.com/photo-1618199901175-5e026466a6cb?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1534&q=80",
      "https://images.unsplash.com/photo-1618204948550-3b60d5668b13?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1534&q=80",
      "https://images.unsplash.com/photo-1618220244721-241b3c831a00?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=3304&q=80",
    ];
    const showGallery = ref(false)

    return { images, showGallery }
  }
})
</script>

<style>
html {
  overflow: hidden;
}
body {
  overflow: auto;
}
html,
body {
  padding: 0;
  margin: 0;
}
</style>