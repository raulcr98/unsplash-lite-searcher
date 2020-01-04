<template>
  <div id="container">
    <form class="form" v-on:submit.prevent>
      <input id="search" type="text" v-model="search" placeholder="Type some keywords" />
      <input class="primary" type="submit" value="Search" v-on:click="fetchimages" :disabled="search == last_search"/>
    </form>
    <div class="images">
      <img v-bind:key="image.id" v-for="image in images" v-bind:src="image.urls.small" alt="" />
    </div>
    <div v-if="images.length > 0" id="load_more">
      <button class="primary" v-if="end == false" v-on:click="load_more"> Load More Cool Images about {{search}} </button>
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
      last_search: '',
      search: '',
      page: 1,
      end: false,
      images: []
    };
  },
  methods: {
    fetchimages: function() {
      if(this.last_search != this.search){
        this.images = [];
        this.end = false;
        this.page = 1;
      }
      axios
      .get(
        "https://api.unsplash.com/search/photos?client_id=" + ID + "&page=" + this.page + "&query=" + this.search + "&per_page=6&order_by=latest"
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
      this.last_search = this.search;
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
#load_more {
  display: flex;
  flex-direction: row;
  justify-content: center;
  margin-bottom: 2em;
}
#load_more > button {
  margin-top: 2em;
}
.primary {
  padding: 1em;
  background: #456990;
  border: none;
  color: #e4fde1;
  border-radius: 5px;
  transition: .3s;
}
.primary:hover {
  background: #114b5f;
}
</style>
