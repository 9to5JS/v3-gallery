<template>
  <teleport v-if="show" to="body">
    <div class="n-grallery-mask" @click="onMask">
      <svg
        v-show="current !== 0 && !isScale"
        class="icon n-grallery-icon n-grallery-left"
        t="1618307357447"
        viewBox="0 0 1024 1024"
        version="1.1"
        xmlns="http://www.w3.org/2000/svg"
        p-id="2966"
        width="48"
        height="48"
        @click.stop="onLeft"
      >
        <path
          d="M820 512c0 17.67-14.33 32-32 32H313.25L484.9 715.65c12.5 12.5 12.5 32.76 0 45.26-6.25 6.25-14.44 9.37-22.63 9.37s-16.38-3.12-22.63-9.37L213.37 534.63c-12.5-12.5-12.5-32.76 0-45.26L439.65 263.1c12.5-12.5 32.76-12.5 45.25 0 12.5 12.5 12.5 32.76 0 45.26L313.25 480H788c17.67 0 32 14.33 32 32z"
          p-id="2967"
          fill="#ffffff"
        />
      </svg>

      <svg
        v-show="current !== images.length - 1 && !isScale"
        t="1618307449295"
        class="icon n-grallery-icon n-grallery-right"
        viewBox="0 0 1024 1024"
        version="1.1"
        xmlns="http://www.w3.org/2000/svg"
        p-id="3229"
        width="48"
        height="48"
        @click.stop="onRight"
      >
        <path
          d="M236 480h474.75L539.1 308.35c-12.5-12.5-12.5-32.76 0-45.26s32.76-12.5 45.25 0l226.27 226.27c12.5 12.5 12.5 32.76 0 45.26L584.35 760.9c-6.25 6.25-14.44 9.37-22.63 9.37s-16.38-3.12-22.63-9.37c-12.5-12.5-12.5-32.76 0-45.26L710.75 544H236c-17.67 0-32-14.33-32-32s14.33-32 32-32z"
          p-id="3230"
          fill="#ffffff"
        />
      </svg>

      <svg
        v-show="!isScale"
        t="1618307594258"
        class="icon n-grallery-icon n-grallery-close"
        viewBox="0 0 1024 1024"
        version="1.1"
        xmlns="http://www.w3.org/2000/svg"
        p-id="4434"
        width="48"
        height="48"
        @click.stop="$emit('update:show', false)"
      >
        <path
          d="M572.16 512l183.466667-183.04a42.666667 42.666667 0 1 0-60.586667-60.586667L512 451.84l-183.04-183.466667a42.666667 42.666667 0 0 0-60.586667 60.586667l183.466667 183.04-183.466667 183.04a42.666667 42.666667 0 0 0 0 60.586667 42.666667 42.666667 0 0 0 60.586667 0l183.04-183.466667 183.04 183.466667a42.666667 42.666667 0 0 0 60.586667 0 42.666667 42.666667 0 0 0 0-60.586667z"
          p-id="4435"
          fill="#ffffff"
        />
      </svg>

      <div class="n-grallery-stage" :style="{ width: `${images.length * 100}%` }">
        <div
          class="n-slide"
          v-for="(src, idx) in images"
          :key="idx"
          :style="{ left: `${idx * 100}%`, transform: `translate3d(${-current * 100}%, 0, 0)` }"
        >
          <VImg :src="src" @change="scaleChange" />
        </div>
      </div>
    </div>
  </teleport>
</template>

<script>
import { defineComponent, ref, watch } from 'vue'
import VImg from './VImg.vue'

export default defineComponent({
  components: {
    VImg
  },

  props: {
    images: {
      type: Array,
      default: () => ([])
    },
    index: {
      type: Number,
      default: 0
    },
    show: {
      type: Boolean,
      default: false
    }
  },

  emits: ['update:show'],

  setup(props, ctx) {
    const current = ref(0)
    const len = ref(0)

    watch(() => props.show, () => {
      current.value = props.index
      len.value = props.images.length
    })

    const onLeft = () => {
      if (current.value >= 0) {
        current.value = current.value - 1
      }
    }
    const onRight = () => {
      if (current.value < len.value) {
        current.value = current.value + 1
      }
    }

    const isScale = ref(false)

    const scaleChange = (val) => {
      isScale.value = val
    }

    const onMask = (e) => {
      // const element = e.target || e.srcElement

      // if (!isScale.value && element.localName !== 'img') {
      //   ctx.emit('update:show', false)
      // }
    }

    return {
      current,
      onLeft,
      onRight,
      scaleChange,
      isScale,
      onMask
    }
  }
})
</script>

<style>
.n-grallery-mask {
  width: 100%;
  height: 100vh;
  background: rgba(0, 0, 0, 1);
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 99999;
}
.n-grallery-icon {
  background: rgba(255, 255, 255, 0.1);
  padding: 8px;
  border-radius: 50%;
  cursor: pointer;
  transition: background 120ms;
  z-index: 10;
  color: #fff;
}
.n-grallery-icon:hover {
  background: rgba(255, 255, 255, 0.2);
}
.n-grallery-left {
  position: fixed;
  top: 50%;
  left: 10px;
  transform: translateY(-50%);
}
.n-grallery-right {
  position: fixed;
  top: 50%;
  right: 10px;
  transform: translateY(-50%);
}
.n-grallery-close {
  position: absolute;
  top: 10px;
  left: 10px;
}
.n-grallery-stage {
  position: relative;
  width: 100%;
  height: inherit;
  overflow: hidden;
}
.n-slide {
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  transition: all 200ms cubic-bezier(0.4, 0, 0.2, 1);
}
</style>