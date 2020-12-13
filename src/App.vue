<template>
  <div id="app">
    <input type="file" @change="imageChange"/>
    <img alt="Image Preview" v-if="filePath" :src="filePath" id="image-preview">
  </div>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  data: function() {
    return {
      filePath: '',
    }
  },
  methods: {
    imageChange(event) {
      this.filePath = URL.createObjectURL(event.target.files[0]);
    },
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
  justify-content: center;
  align-items: center;
}

#image-preview {
  width: 300px;
  height: auto;
}
</style>
