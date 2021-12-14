<template>
<a href="www.google.si">
<div class="card" style="width: 18rem;">
  <img class="card-img-top" src="https://fakeimg.pl/300/" alt="Card image cap">
  <div class="card-body">
    <h5 class="card-title">{{userFullName}}</h5>
        <p class="card-text">{{userName}}</p>
    <p class="card-text">{{userId}}</p>
  </div>
</div>
  </a>
  <p :v-bind="randomAlbumID()">{{randomAlbumID()}}</p>
</template>

<script>
import axios from "axios";

export default {
  props:{
    userName: String,
    userId: Number,
    userFullName : String
  },
  name: "Users",
  data() {
    return {
//       users_api: "https://jsonplaceholder.typicode.com/users",
//       users: [],
      albums_endpoint: "https://jsonplaceholder.typicode.com/",
      albums: [],
//       photos_api: "https://jsonplaceholder.typicode.com/albums/1/photos",
//       user_id: [],
//       photos: []
     };
   },
  mounted() {
    axios
      .get(`${this.albums_endpoint}users/${this.userId}/albums `)
      .then(({ data }) => {
        this.albums = data;
      })
      .catch((e) => {
        console.log(e);
      });
  },
  methods: {
    randomAlbumID(){
        return this.albums[Math.floor(Math.random() * this.albums.length)];
    }
  }
//   methods: {
//     // randPhoto = () => photos[Math.floor(Math.random() * photos.length)]
//   }
};
</script>

<style>

</style>