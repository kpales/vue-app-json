<template>
  <img
    class="card-img-top"
    :src="random_photo"
    alt="Card image cap"
    :v-bind=randomPhotoId()
  />
  <p>RandomAlbum prop-getted :{{ random_album }}</p>
  <p>Random Album data : {{ random_photo }}</p>
  <p>Photos endpoint : {{photos_endpoint}}</p>
</template>

<script>
import axios from "axios";
export default {
  props: {
    randomAlbum: Number,
  },
  name: "RandomProfilePhoto",
  data() {
    return {
              random_album: this.randomAlbum,
      //   photos_endpoint: "https://jsonplaceholder.typicode.com",
      photos_endpoint: `https://jsonplaceholder.typicode.com/albums/${this.randomAlbum}/photos`,
      photo: [],
      random_photo: "",
    };
  },
  created(){
 
  },
  mounted() {
               console.log("RandomAlbum: " + this.randomAlbum);
           console.log("Photos_endpoint" + this.photos_endpoint);
           console.log("random_album: " + this.random_album)

        //   console.log(this.randomAlbum);
        //  console.log(this.photos_endpoint);

    axios
      .get(this.photos_endpoint)
      .then(({ data }) => {
        data.forEach((item) => this.photo.push(item.url));
      })
      // .then(response => this.photo = response)
      .catch((e) => {
        console.log(e);
      });console.log(this.photo)
  },
  methods: {
    randomPhotoId() {
        this.random_photo =
        this.photo[Math.floor(Math.random() * this.photo.length)];
        console.log(this.random_photo);
      return this.random_photo
    },
  },
};
</script>

<style>
</style>