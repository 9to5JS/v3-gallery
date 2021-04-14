<template>
  <div class="v-img" :class="[isScale ? 'v-is-scale' : '']" @click="onWrapper">
    <img
      :src="src"
      :class="[canScale && !isScale ? 'v-can-scale' : '']"
      loading="lazy"
      ref="imgRef"
    />
  </div>
</template>

<script>
import { defineComponent, ref } from 'vue'

export default defineComponent({
  props: {
    src: {
      type: String,
      default: true
    }
  },

  emits: ['change'],

  setup(props, ctx) {
    const canScale = ref(false)
    const isScale = ref(false)
    const imgRef = ref()
    const windowHeight = window.innerHeight

    const realHeight = ref(0)

    const init = () => {
      if (props.src) {
        const img = new Image()
        img.src = props.src
        img.onload = () => {
          if (img.height > windowHeight) {
            canScale.value = true
            realHeight.value = img.height
          }
        }
      }
    }
    init()

    const onImg = () => {
      if (!canScale.value) return

      if (!isScale.value) {
        imgRef.value.style.height = realHeight.value + 'px'
        isScale.value = true
      }
    }

    const onWrapper = (e) => {
      if (!canScale.value) return

      const element = e.target || e.srcElement
      if (!isScale.value && element.localName === 'img') {
        imgRef.value.style.height = realHeight.value + 'px'
        isScale.value = true
        ctx.emit('change', isScale.value)
        return
      }
      if (isScale.value) {
        imgRef.value.style.height = 'inherit'
        isScale.value = false
        ctx.emit('change', isScale.value)
        return
      }
    }

    return {
      imgRef,
      onImg,
      canScale,
      isScale,
      onWrapper
    }
  },
})
</script>

<style>
.v-fixed {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 100000;
  background: #000;
}
.v-img {
  width: 100%;
  max-height: 100vh;
  overflow: auto;
  display: flex;
  justify-content: center;
}
.v-img img {
  user-select: none;
  height: inherit;
}

.v-can-scale {
  cursor: zoom-in;
}
.v-is-scale {
  cursor: zoom-out;
}
</style>
