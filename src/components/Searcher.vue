<template>
  <div id="container">
    <form class="form" v-on:submit.prevent>
      <input id="search" type="text" v-model="search" />
      <input type="submit" value="Search" v-on:click="fetchimages" />
    </form>
    <div>
      <img v-bind:key="image.id" v-for="image in images" v-bind:src="image.urls.small" alt="" />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import { ID } from '../env.js';

export default {
  name: "container",
  data() {
    return {
      search: '',
      images: []
    };
  },
  methods: {
    fetchimages: function() {
      axios
      .get("https://api.unsplash.com/search/photos?client_id=" + ID + "&page=1&query=" + this.search + "&per_page=3")
      .then(response => (this.images = response.data.results));
    }
  },
  props: {}
};
</script>

<style>
.form {
  display: flex;
  flex-direction: row;
  justify-content: center;
}
.form > * {
  margin-left: 1em;
  margin-right: 1em;
}
#search {
  width: 300px;
  padding: 1em;
}
</style>
