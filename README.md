<h1 align="center">
  V3 Gallery
</h1>

<p align="center">
<img src="https://img.shields.io/npm/v/v3-gallery?color=blue">
<img src="https://img.shields.io/npm/l/v3-gallery">
<img src="https://img.shields.io/npm/dw/v3-gallery">
</p>

<div align="center">
V3 Gallery is a Vue 3 gallery component based on TypeScript & Composition API.
</div>

<br>
<br>

English | [简体中文](./README-zh_CN.md)

## Install

```
npm install v3-gallery
```

```
pnpm add v3-gallery
```

```
yarn add v3-gallery
```

## Usage

```
<template>
  <button @click="show = true">Open</button>
  <VGaller v-model="show" :images="images" />
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'
import VGaller from 'v3-gallery'

export default defineComponent({
  name: 'App',

  components: {
    VGaller
  },

  setup() {
    const show = ref(false)
    const images = [
      "https://xxxxx.jpg",
      "https://xxxxxxxxx.jpg"
    ]

    return { show, images }
  }
})
</script>
```

## License

[MIT](https://github.com/inhal/v3-gallery/blob/main/LICENSE)
