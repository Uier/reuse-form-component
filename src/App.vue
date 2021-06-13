<template>
  <post-form @submit="newPost" />
  <Posts :posts="posts" @update-post="updatePost" />
</template>

<script setup>
import { ref } from 'vue';
import Posts from './components/posts.vue';
import PostForm from './components/post-form.vue';

const posts = ref([
  {
    id: 1,
    title: 'First post',
    content: 'This is the first one',
    author: 'Alice',
  },
  {
    id: 2,
    title: 'Second post',
    content: 'This is the second one',
    author: 'Bob',
  },
]);

const newPost = (post) => {
  posts.value.push(Object.assign({ id: posts.value.length + 1 }, post));
};

const updatePost = (index, post) => {
  posts.value[index] = Object.assign({}, post);
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
