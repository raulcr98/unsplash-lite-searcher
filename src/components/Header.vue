<template>
  <div class="header">
    <ul>
      <li>
        <h1>Unsplash-Lite-Searcher</h1>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Header",
  props: {}
};
</script>

<style>
ul {
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
  align-items: baseline;
}
li {
  list-style: none;
}
</style>
