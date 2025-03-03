# Vue Image Background Component

A Vue.js component that provides a flexible image background system with configuration-based fallback support. This component allows you to display images as backgrounds while maintaining the ability to render child components within the background container.

## Features

- Dynamic image background loading
- Configuration-based image management
- Automatic fallback to asset images
- Support for child components via slots
- Responsive background sizing
- Error handling for missing images

## Installation

```sh
npm install
```

## Usage

1. Place your images in the following directories:
   - Configuration images: `public/configurations/`
   - Fallback images: `public/assets/`

2. Import and use the component in your Vue files:

```vue
<template>
  <ImageBackground imageName="your-image.jpg">
    <!-- Your content here -->
    <div>This content will be displayed over the background image</div>
  </ImageBackground>
</template>

<script>
import ImageBackground from './components/ImageBackground.vue'

export default {
  components: {
    ImageBackground
  }
}
</script>
```

## How it Works

The component follows this logic:
1. First attempts to load the image from the configurations folder
2. If the configuration image is not found, falls back to the assets folder
3. If neither image is found, logs an error to the console

## Development

```sh
npm run dev
```

## Building for Production

```sh
npm run build
```

## Recommended IDE Setup

[VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and disable Vetur).
