<template>
<a href="www.google.si">
<div class="card" style="width: 18rem;" v-bind = randomAlbumID()>
  <RandomProfilePhoto
    :random-album = randomAlbum
   />
  <div class="card-body">
    <h5 class="card-title">{{userFullName}}</h5>
        <p class="card-text">{{userName}}</p>
    <p class="card-text">{{userId}}</p>
  </div>
</div>
  </a>
</template>

<script>
import axios from "axios";
import RandomProfilePhoto from "@/components/RandomProfilePhoto.vue";

export default {
  components:{
    RandomProfilePhoto
  },
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
      randomAlbum :null
//       photos_api: "https://jsonplaceholder.typicode.com/albums/1/photos",
//       user_id: [],
//       photos: []
     };
   },
  mounted() {
    axios
      .get(`${this.albums_endpoint}users/${this.userId}/albums `)
      .then(({ data }) => { data.forEach( (item) => this.albums.push(item.id) )
        // this.albums = data;
      })
      .catch((e) => {
        console.log(e);
      });
  },
  methods: {
    randomAlbumID(){
         return this.randomAlbum = this.albums[Math.floor(Math.random() * this.albums.length)];
        
    }
  }
//   methods: {
//     // randPhoto = () => photos[Math.floor(Math.random() * photos.length)]
//   }
};
</script>

<style>

</style>