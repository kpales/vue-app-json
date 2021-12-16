<template>
  <div class="container">
    <div class="row">
      <div class="album" v-for="album in albums" :key = album.id>
          <p>Test</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  inject: ["albums"],
};
</script>

<style>
</style>