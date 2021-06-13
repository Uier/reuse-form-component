<template>
  <h1>Posts</h1>
  <div
    style="display: flex; flex-direction: column; align-items: center"
  >
    <div
      v-for="(post, index) in posts"
      :key="post.id"
      style="margin-top: 20px"
    >
      <div
        style="border: 1px solid #000; padding: 10px; width: 400px"
      >
        {{ `# ${post.id}: ${post.title}` }}
        <div>
          <p>{{ post.content }}</p>
        </div>
        <div>
          <p>{{ `posted by ${post.author}` }}</p>
        </div>
        <post-form :populateWith="post" @submit="(modifiedPost) => submit(index, modifiedPost)" />
      </div>
    </div>
  </div>
</template>

<script setup>
import { defineProps, defineEmit, toRefs } from 'vue';
import PostForm from './post-form.vue';

const props = defineProps({
  posts: {
    type: Array,
    required: true,
  },
});
const { posts } = toRefs(props);
const emit = defineEmit(['update-post']);

const submit = (index, post) => {
  emit('update-post', index, post);
};
</script>

<style scoped>
a {
  color: #42b983;
}
</style>
