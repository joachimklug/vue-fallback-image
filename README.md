# Vue Image Background Component

A Vue.js component that provides a flexible image background system with configuration-based fallback support. This component allows you to display images as backgrounds while maintaining the ability to render child components within the background container.

## Features

- Dynamic image background loading
- Configuration-based image management
- Automatic fallback to asset images
- Support for child components via slots
- Responsive background sizing
- Error handling for missing images
- Configurable image paths
- Fully customizable background styles
- Custom CSS class support

## Installation

```sh
npm install
```

## Usage

1. Place your images in the following directories (default paths):
   - Configuration images: `public/configurations/`
   - Fallback images: `public/assets/`

2. Import and use the component in your Vue files:

```vue
<template>
  <!-- Basic usage with default styles -->
  <ImageBackground imageName="your-image.jpg">
    <div>This content will be displayed over the background image</div>
  </ImageBackground>

  <!-- Custom paths -->
  <ImageBackground 
    imageName="your-image.jpg"
    configPath="/custom/config/path"
    assetPath="/custom/asset/path"
  >
    <div>Content with custom image paths</div>
  </ImageBackground>

  <!-- Custom background styles -->
  <ImageBackground 
    imageName="your-image.jpg"
    :backgroundStyle="{
      backgroundSize: 'contain',
      backgroundPosition: 'top left',
      backgroundColor: '#f0f0f0'
    }"
  >
    <div>Content with custom background styles</div>
  </ImageBackground>

  <!-- Custom CSS class -->
  <ImageBackground 
    imageName="your-image.jpg"
    className="custom-background"
  >
    <div>Content with custom CSS class</div>
  </ImageBackground>

  <!-- Combined styles and class -->
  <ImageBackground 
    imageName="your-image.jpg"
    className="custom-background"
    :backgroundStyle="{
      backgroundSize: 'contain',
      backgroundPosition: 'top left'
    }"
  >
    <div>Content with both custom styles and class</div>
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

<style>
.custom-background {
  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}
</style>
```

## Props

| Prop | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| imageName | String | Yes | - | The name of the image file to load |
| configPath | String | No | '/configurations' | The path to look for configuration images |
| assetPath | String | No | '/assets' | The fallback path for asset images |
| backgroundStyle | Object | No | See below | Custom CSS styles for the background |
| className | String | No | '' | Custom CSS class to apply to the component |

## Default Background Styles

The component provides these default styles if none are specified:
```javascript
{
  backgroundSize: 'cover',
  backgroundPosition: 'center',
  backgroundRepeat: 'no-repeat'
}
```

You can override these defaults by providing your own `backgroundStyle` object. The component will automatically add the `backgroundImage` property based on the loaded image.

## How it Works

The component follows this logic:
1. First attempts to load the image from the configuration path (default: `/configurations/`)
2. If the configuration image is not found, falls back to the asset path (default: `/assets/`)
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
