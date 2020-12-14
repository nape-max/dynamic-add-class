<template>
  <div id="app">
    <div id="photo-editor">
      <div id="preview">
        <img
          alt="Image Preview"
          v-if="filePath && isDisplayImage"
          :src="filePath"
          :style="imageSizeStyles"
          :class="imageClasses"
          id="image-preview"
        />
      </div>
      <div id="control-buttons">
        <input 
          type="file"
          @change="imageChange"
        />
        <div id="style-buttons">
          <input 
            type="button"
            :class="imageClasses.border ? 'active' : ''"
            @click="changeBorderClass"
            value="Рамка"
          />
          <input 
            type="button"
            :class="imageClasses.shadow ? 'active' : ''"
            @click="changeShadowClass"
            value="Тень"
          />
          <input
            type="button"
            :class="imageClasses.small ? 'active' : ''"
            @click="changeSmallClass"
            value="Уменьшить размер"
          />
        </div>
        <div class="input-range-flex">
          <label for="inputWidth">Ширина: {{ imageSizes.currentWidth }}</label>
          <input 
            id="inputWidth"
            type="range"
            min="0"
            :max="imageSizes.maxWidth"
            :value="imageSizes.currentWidth"
            :disabled="imageClasses.small ? true : false"
            @input="imageSizes.currentWidth = $event.target.value"
          />
        </div>
        <div class="input-range-flex">
          <label for="inputHeight">Высота: {{ imageSizes.currentHeight }}</label>
          <input
            id="inputHeight"
            type="range"
            min="0"
            :max="imageSizes.maxHeight"
            :value="imageSizes.currentHeight"
            :disabled="imageClasses.small ? true : false"
            @input="imageSizes.currentHeight = $event.target.value"
          />
        </div>
        <input
          type="button"
          :class="!isDisplayImage ? 'active' : ''"
          value="Скрыть изображение"
          @click="imageHideShow"
        />
      </div>
    </div>
  </div>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  data: function() {
    return {
      filePath: '',
      imageSizes: {
        maxWidth: 300,
        maxHeight: 200,
        currentWidth: 300,
        currentHeight: 200,
      },
      imageClasses: {
        border: false,
        shadow: false,
        small: false,
      },
      isDisplayImage: true,
    }
  },
  computed: {
    imageSizeStyles() {
      return {
        width: `${this.imageSizes.currentWidth}px`,
        height: `${this.imageSizes.currentHeight}px`
      };
    }
  },
  methods: {
    imageChange(event) {
      this.filePath = URL.createObjectURL(event.target.files[0]);
    },
    changeBorderClass() {
      this.imageClasses.border = !this.imageClasses.border;
      console.log(this.imageClasses)
    },
    changeShadowClass() {
      this.imageClasses.shadow = !this.imageClasses.shadow;
    },
    changeSmallClass(event) {
      this.imageClasses.small = !this.imageClasses.small;
      event.target.value = this.imageClasses.small ? "Увеличить размер" : "Уменьшить размер";
    },
    imageHideShow(event) {
      this.isDisplayImage = !this.isDisplayImage;
      event.target.value = this.isDisplayImage ? "Скрыть изображение" : "Показать изображение";
    }
  },
  components: {
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;

  display: flex;
  flex-direction: column;
  align-items: center;
}

#photo-editor {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;

  width: 600px;
  height: 200px;
}

#preview {
  width: 50%;
  height: 100%;
}

#image-preview {
  width: 100%;
  height: 100%;
}

#control-buttons {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  text-align: left;

  height: 100%;
  width: 45%;

  padding: 0 10px;
}

#style-buttons {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}

.input-range-flex {
  display: flex;
  flex-direction: column;
}

.border {
  border: 2px dashed black;
}

.shadow {
  box-shadow: 5px 5px 8px rgba(0,0,0, 0.5);
}

.small {
  width: 60% !important;
  height: 55% !important;
}

.active {
  background-color: #bbb;
}
</style>
