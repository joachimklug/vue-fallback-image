<template>
    <div :class="className" :style="computedBackgroundStyle">
      <slot></slot>
    </div>
  </template>
  
  <script>
  export default {
    name: 'ImageBackground',
    props: {
      imageName: {
        type: String,
        required: true
      },
      configPath: {
        type: String,
        default: '/configurations'
      },
      assetPath: {
        type: String,
        default: '/assets'
      },
      backgroundStyle: {
        type: Object,
        default: () => ({
          backgroundSize: 'cover',
          backgroundPosition: 'center',
        })
      },
      className: {
        type: String,
        default: ''
      }
    },
    data() {
      return {
        imageUrl: null
      }
    },
    computed: {
      computedBackgroundStyle() {
        return {
          ...this.backgroundStyle,
          backgroundImage: this.imageUrl ? `url(${this.imageUrl})` : 'none'
        }
      }
    },
    async mounted() {
      try {
        // Try to load from configurations first
        const configImagePath = `${this.configPath}/${this.imageName}`;
        const configExists = await this.checkImage(configImagePath);
  
        if (configExists) {
          this.imageUrl = configImagePath;
        } else {
          // Fallback to assets
          const assetImagePath = `${this.assetPath}/${this.imageName}`;
          const assetExists = await this.checkImage(assetImagePath);
          if (assetExists) {
            this.imageUrl = assetImagePath;
          } else {
            console.error(`Neither configuration nor asset image found for: ${this.imageName}`);
          }
        }
      } catch (error) {
        console.error(`Failed to load image: ${this.imageName}`, error);
      }
    },
    methods: {
      checkImage(url) {
        return new Promise((resolve) => {
          const img = new Image();
          img.onload = () => resolve(true);
          img.onerror = () => resolve(false);
          img.src = url;
        });
      }
    }
  }
  </script>