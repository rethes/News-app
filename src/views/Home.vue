<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <Posts/>
    <CreatePosts/>
  </div>
</template>

<script>
// @ is an alias to /src
import Posts from '../components/posts.vue';
import CreatePosts from '../components/CreatePosts.vue';

export default {
  name: 'home',
  components: {
    Posts,
    CreatePosts,
  },
};
</script>
