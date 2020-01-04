<template>
  <div id="container">
    <form class="form" v-on:submit.prevent>
      <input id="search" type="text" v-model="search" />
      <input type="submit" value="Search" v-on:click="fetchimages" />
    </form>
    <div class="images">
      <img v-bind:key="image.id" v-for="image in images" v-bind:src="image.urls.small" alt="" />
      <span v-if="loading">Loading ...</span>
    </div>
    <div v-if="images.length > 0">
      <button v-if="end == false" v-on:click="load_more"> Load More Cool Images about {{search}} </button>
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
      loading: false,
      page: 1,
      end: false,
      images: []
    };
  },
  methods: {
    fetchimages: function() {
      this.loading = true;
      axios
      .get(
        "https://api.unsplash.com/search/photos?client_id=" + ID + "&page=" + this.page + "&query=" + this.search + "&per_page=2&order_by=latest"
      )
      .then(response => {
        response.data.results.map(image => {
          this.images.push(image);
        });
      })
      .catch(e => {
        this.end = true;
        console.log(e);
      });
      this.loading = false;
    },
    load_more: function() {
      this.page += 1;
      this.fetchimages();
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
.images {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: space-evenly;
  align-items: center;
}
.images > img {
  margin: 1em;
  border-radius: 1em;
  transition: .3s ease all;
}
.images > img:hover {
  box-shadow: 1px 1px 20px rgba(1, 1, 1, .4);
  transform: scale(1.01);
}
</style>
