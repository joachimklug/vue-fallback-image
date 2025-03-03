<template>
  <div class="image-background" :style="backgroundStyle">
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
    }
  },
  data() {
    return {
      imageUrl: null
    }
  },
  computed: {
    backgroundStyle() {
      return {
        backgroundImage: this.imageUrl ? `url(${this.imageUrl})` : 'none',
        backgroundSize: 'cover',
        backgroundPosition: 'center',
        backgroundRepeat: 'no-repeat'
      }
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
  },
  async mounted() {
    try {
      // Try to load from configurations first
      const configPath = `/configurations/${this.imageName}`;
      const configExists = await this.checkImage(configPath);
      
      if (configExists) {
        this.imageUrl = configPath;
      } else {
        // Fallback to assets
        const assetsPath = `/assets/${this.imageName}`;
        const assetExists = await this.checkImage(assetsPath);
        if (assetExists) {
          this.imageUrl = assetsPath;
        } else {
          console.error(`Neither configuration nor asset image found for: ${this.imageName}`);
        }
      }
    } catch (error) {
      console.error(`Failed to load image: ${this.imageName}`, error);
    }
  }
}
</script>

<style scoped>
.image-background {
  position: relative;
  width: 100%;
  height: 100%;
  min-height: 200px;
}
</style> 