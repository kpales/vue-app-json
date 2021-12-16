<template>
  <router-link :to="'/' + userId + '/album/'">
  <div class="card" style="width: 18rem" v-bind=randomAlbumID()>
    <RandomProfilePhoto
     v-if="random_album"
      :random-album="random_album"
       />
    <div class="card-body">
      <h5 class="card-title">{{ userFullName }}</h5>
      <p class="card-text">{{ userName }}</p>
      <p class="card-text">{{ userId }}</p>
      <p>Random album from UserDetail: {{ random_album }}</p>
      <p>Random album function from UserDetail: {{ randomAlbumID() }}</p>
      <p> Data props albums[] : {{albums}}</p>
    </div>
  </div>
  </router-link>
</template>

<script>
import axios from "axios";
import RandomProfilePhoto from "@/components/RandomProfilePhoto.vue";

export default {
  components: {
    RandomProfilePhoto,
  },
  props: {
    userName: String,
    userId: Number,
    userFullName: String,
  },
  name: "Users",
  data() {
    return {
      albums_endpoint: `https://jsonplaceholder.typicode.com/users/${this.userId}/albums`,
      albums: [],
      random_album: null,
    };
  },
  mounted() {
    axios
      .get(this.albums_endpoint)
      .then(({ data }) => {
        data.forEach((item) => this.albums.push(item.id));
      })
      .catch((e) => {
        console.log(e);
      });
  },
  methods: {
    randomAlbumID() {
      return this.random_album =this.albums[Math.floor(Math.random() * this.albums.length)];
    },
  },
  provide(){
    return{
      albums: this.albums
    }
  }
};
</script>

<style>
a{
  text-decoration:none;
  color:black;
}
</style>