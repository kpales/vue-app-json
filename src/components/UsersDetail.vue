<template>
  <!-- <a href="www.google.si"> -->
  <div class="card" style="width: 18rem" v-bind=randomAlbumID()>
    <RandomProfilePhoto v-if="random_album" :random-album="random_album" />
    <div class="card-body">
      <h5 class="card-title">{{ userFullName }}</h5>
      <p class="card-text">{{ userName }}</p>
      <p class="card-text">{{ userId }}</p>
      <p>Random album from UserDetail: {{ random_album }}</p>
      <p>Random album function from UserDetail: {{ randomAlbumID() }}</p>
    </div>
  </div>
  <!-- </a> -->
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
};
</script>

<style>
</style>