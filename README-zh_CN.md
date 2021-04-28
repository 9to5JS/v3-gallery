<h1 align="center">
  V3 Gallery
</h1>

<p align="center">
<img src="https://img.shields.io/npm/v/v3-gallery?color=blue">
<img src="https://img.shields.io/npm/l/v3-gallery">
<img src="https://img.shields.io/npm/dw/v3-gallery">
</p>

<div align="center">
一个 Vue 3 图库，使用 TypeScript 和 Composition API 编写。
</div>

<br>
<br>

[English](./README.md) | 简体中文

## 安装

```
npm install v3-gallery
```

```
pnpm add v3-gallery
```

```
yarn add v3-gallery
```

## 使用

```
<template>
  <button @click="show = true">Open</button>
  <VGaller v-model="show" :images="images" :index="index" />
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
    const index = ref(0) // index, 从 0 到 images 长度减 1
    const images = [
      "https://xxxxx.jpg",
      "https://xxxxxxxxx.jpg"
    ]

    return { show, images, index }
  }
})
</script>
```

## 许可证

[MIT](https://github.com/inhal/v3-gallery/blob/main/LICENSE)
