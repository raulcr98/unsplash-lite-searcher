<template>
  <div class="header">
    <ul>
      <li>
        <h1>Unsplash-Lite-Searcher</h1>
      </li>
      <li>Made by <a href="https://raulcr98.github.io/mysite">raulcr98</a></li>
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
h1 {
  color: #114b5f;
}
</style>
