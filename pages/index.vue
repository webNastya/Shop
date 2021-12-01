<template>
  <div id="app">
    <Header />
    <Container />
  </div>
</template>

<script>
export default {
  name: "app",
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  font-family: "Source Sans Pro", sans-serif;
}
html {
  background-color: rgba(255, 254, 251, 0.8);
}
h1 {
  font-weight: 600;
}
#app {
  max-width: 1420px;
  margin: auto;
}
.container {
  display: flex;
}
</style>
