<template>
<div>
    <h1>{{ msg }}</h1>
    <a href="http://localhost:8888" class="btn btn-primary">Log in with Spotify</a>
</div>
</template>

<script>
export default {
  name: 'Home',
  props: {
    msg: String
  }
}
</script>

<style>

</style>