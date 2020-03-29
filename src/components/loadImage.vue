<template>
  <div class="col-md-12 imageGallery">
    <div class="col-md-12">
      <div class="box">
        <input type="file" style="display:none" @change="onChange($event)" ref="file" />
        <button @click="$refs.file.click()" class="btn btn-light">SELECT IMAGE</button>
      </div>
    </div>
    <div class="clear"></div>
    <images>
      <div class="col-md-12">
        <div class="image" v-for="(image,index) in images" :key="index">
          <img :src="image.url" />
        </div>
      </div>
    </images>
  </div>
</template>
<script>
import { eventBus } from "../main";
import images from "./images";
export default {
  components: {
    images
  },
  data: () => {
    return {
      images: [],
      readySave: true
    };
  },
  methods: {
    onChange(e) {
      const file = e.target.files[0];
      this.images.push({ url: URL.createObjectURL(file) });
      eventBus.$emit("readySave", this.readySave);
      eventBus.$emit("saveButton", this.images);
    }
  }
};
</script>