<template>
  <div class="vg-img-wrapper">
    <img
      :src="src"
      class="vg-img"
      :class="{
        'vg-zoom-in': canScale,
        'vg-zoom-out': isScale
      }"
      style="max-width: 100%; max-height: 100%"
      loading="lazy"
      ref="imgRef"
      @click="onImg"
    />
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";

export default defineComponent({
  props: {
    src: {
      type: String,
      default: ''
    }
  },

  setup(props) {
    const canScale = ref(false)
    const isScale = ref(false)
    const imgRef = ref<HTMLImageElement>()
    const windowHeight = window.innerHeight

    const init = () => {
      if (props.src) {
        const img = new Image()
        img.src = props.src
        img.onload = () => {
          if (img.height > windowHeight) {
            canScale.value = true
          }
        }
      }
    }
    init()

    const onImg = () => {
      if (!canScale.value) return
      if (!imgRef.value) return

      if (!isScale.value) {
        imgRef.value.style.maxWidth = ''
        imgRef.value.style.maxHeight = ''
        isScale.value = true
      } else {
        imgRef.value.style.maxWidth = '100%'
        imgRef.value.style.maxHeight = '100%'
        isScale.value = false
      }
    }

    return {
      canScale,
      isScale,
      imgRef,
      onImg
    }
  }
})
</script>

<style>
.vg-img-wrapper {
  width: 100%;
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  overflow-y: auto;
}
.vg-img {
  user-select: none;
}

.vg-zoom-in {
  cursor: zoom-in;
}
.vg-zoom-out {
  cursor: zoom-out;
}
</style>