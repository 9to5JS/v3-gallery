<template>
  <transition>
    <teleport v-if="modelValue" to="body">
      <div class="vg-mask">
        <svg
          v-show="current !== 0"
          class="icon vg-left"
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
          v-show="images.length && current !== images.length - 1"
          t="1618307449295"
          class="icon vg-right"
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
          t="1618646443970"
          class="icon vg-close"
          viewBox="0 0 1024 1024"
          version="1.1"
          xmlns="http://www.w3.org/2000/svg"
          p-id="1128"
          width="48"
          height="48"
          @click.stop="$emit('update:modelValue', false)"
        >
          <path
            d="M507.168 473.232L716.48 263.936a16 16 0 0 1 22.624 0l11.312 11.312a16 16 0 0 1 0 22.624L541.12 507.168 750.4 716.48a16 16 0 0 1 0 22.624l-11.312 11.312a16 16 0 0 1-22.624 0L507.168 541.12 297.872 750.4a16 16 0 0 1-22.624 0l-11.312-11.312a16 16 0 0 1 0-22.624l209.296-209.312-209.296-209.296a16 16 0 0 1 0-22.624l11.312-11.312a16 16 0 0 1 22.624 0l209.296 209.296z"
            p-id="1129"
            fill="#ffffff"
          />
        </svg>

        <div class="vg-stage">
          <template v-for="(img, idx) in images" :key="idx">
            <VImg v-show="current === idx" :src="img" />
          </template>
        </div>
      </div>
    </teleport>
  </transition>
</template>

<script lang="ts">
import { defineComponent, PropType, ref, watch } from 'vue'
import VImg from './VImg.vue'

export default defineComponent({
  components: {
    VImg
  },

  props: {
    images: {
      type: Array as PropType<string[]>,
      default: () => ([])
    },

    modelValue: {
      type: Boolean,
      default: false
    },

    index: {
      type: Number,
      default: 0
    }
  },

  emits: ['update:modelValue'],

  setup(props) {
    const current = ref(0)
    current.value = props.index
    let len = 0

    watch(() => props.modelValue, () => {
      len = props.images.length
    })

    watch(() => props.index, (val) => current.value = val)

    const onLeft = () => {
      if (current.value >= 0) {
        current.value = current.value - 1
      }
    }
    const onRight = () => {
      if (current.value < len) {
        current.value = current.value + 1
      }
    }

    return {
      current,
      onLeft,
      onRight
    }
  }
})
</script>

<style>
@import url("./index.css");
</style>