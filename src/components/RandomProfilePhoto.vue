<template>
  <img
    class="card-img-top"
    :src="random_photo"
    alt="Card image cap"
    :v-bind="randomPhoto()"
  />
  {{ randomAlbum }}
  {{random_photo}}
</template>

<script>
import axios from "axios";
export default {
  props: {
    randomAlbum: Number,
  },
  name:"RandomProfilePhoto",
  data() {
    return {
      photos_endpoint: "https://jsonplaceholder.typicode.com",
      url: "https://jsonplaceholder.typicode.com/albums/1/photos",
      photo: [],
      random_photo : ''
    };
  },
  mounted() {
    axios
      .get(`${this.photos_endpoint}/albums/${this.randomAlbum}/photos`)
      .then(({ data }) => {data.forEach( (item) => this.photo.push(item.url) )
        // this.photo = data;
        // console.log(this.photo)
      })
      .catch((e) => {
        console.log(e);
      });
  },
    methods: {
    randomPhoto(){
        this.random_photo = this.photo[Math.floor(Math.random() * this.photo.length)];
        // console.log(this.photo.length)
        
    }
  }
};
</script>

<style>
</style>