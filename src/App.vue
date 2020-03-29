<template>
  <div class="container">
    <div class="row">
      <component :is="selectedComponent">
        <saveImage v-for="(arrayImg,index) in arrayImage" :key="index">{{arrayImg.url}}</saveImage>
      </component>

      <div class="col-md-12 text-right buttonSave mt-1" v-if="truePut">
        <button @click="showJson" class="btn btn-danger">Save</button>
      </div>
    </div>
  </div>
</template>

<script>
import { eventBus } from "./main";
import loadImage from "./components/loadImage";
import saveImage from "./components/saveImage";
export default {
  components: {
    loadImage,
    saveImage
  },
  data: () => {
    return {
      truePut: false,
      selectedComponent: "loadImage",
      arrayImage: []
    };
  },
  created() {
    eventBus.$on("readySave", readySave => {
      this.truePut = readySave;
    });
    eventBus.$on("saveButton", arrayImage => {
      this.arrayImage = arrayImage;
    });
  },
  methods: {
    showJson() {
      this.selectedComponent = "saveImage";
      this.truePut = false;
    }
  }
};
</script>

<style >
body {
  margin: 20px 0;
  transition: 1s;
}

.imageGallery {
  width: 100%;
  height: auto;
  padding: 30px;
  border: 1px solid #eee;
  border-radius: 10px 0 10px 0;
  box-shadow: 0px 3px 5px rgba(238, 238, 238, 1);
}

.box {
  width: 100%;
  height: 150px;
  border: 1px solid #eee;
  border-radius: 5px;
  float: left;
}
.box button {
  width: 100%;
  height: 150px;
  color: #d2d2d2;
  font-size: 30px;
  transition: 500ms;
}
.box button:hover {
  color: #333;
  background: #f2f2f2;
}

.image {
  width: 15%;
  height: auto;
  border: 1px solid #f2f2f2;
  border-radius: 10px;
  transition: 500ms;
  float: left;
  margin: 20px 5px;
}
.image:hover,
.image img:hover {
  box-shadow: 0px 4px 5px #ddd;
}
.image img {
  width: 100%;
  height: auto;
  border-radius: 10px;
}
.buttonSave button {
  padding: 5px 20px;
  border-radius: 10px 0 10px 0;
}
.clear {
  clear: both;
}
</style>