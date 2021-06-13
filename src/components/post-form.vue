<template>
  <button @click="openModal">{{ activator }}</button>
  <div id="myModal" class="modal" v-if="showModal">
    <!-- Modal content -->
    <div class="modal-content">
      <span class="close" @click="closeModal">&times;</span>
      <div
        style="display: flex; flex-direction: column; justify-content: space-around; align-items: center; height: 150px"
      >
        <input type="text" placeholder="title" v-model="post.title">
        <input type="text" placeholder="content" v-model="post.content">
        <input type="text" placeholder="author" v-model="post.author">
        <button @click="submit">submit</button>
        <button @click="generatePost">gen post</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { defineProps, defineEmit, ref, toRefs, computed } from 'vue';

// interface Post {
//   id?: number
//   title: string
//   content: string
//   author: string
// }

const props = defineProps({
  populateWith: {
    type: Object,
    default: () => ({
      title: '',
      content: '',
      author: '',
    }),
  },
});
const { populateWith } = toRefs(props);
const emit = defineEmit(['submit']);

const post = ref(null);
const showModal = ref(false);
const activator = computed(() => {
  return populateWith.value.id ? `Edit post` : 'New post'; 
});

const openModal = () => {
  post.value = Object.assign({}, populateWith.value);
  showModal.value = true;
};
const closeModal = () => showModal.value = false;
const submit = () => {
  emit('submit', post.value);
  closeModal();
};
const generatePost = () => {
  post.value.title = generateString(8);
  post.value.content = generateString(20);
  post.value.author = generateString(6);
}
const generateString = (length) => {
  let result = '';
  const characters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
  const charactersLength = characters.length;
  for ( var i = 0; i < length; i++ ) {
    result += characters.charAt(Math.floor(Math.random() * charactersLength));
  }
  return result;
};
</script>

<style scoped>
.modal {
  display: block; /* Hidden by default */
  position: fixed; /* Stay in place */
  z-index: 1; /* Sit on top */
  left: 0;
  top: 0;
  width: 100%; /* Full width */
  height: 100%; /* Full height */
  background-color: rgba(0,0,0,0.4); /* Black w/ opacity */
}

/* Modal Content/Box */
.modal-content {
  background-color: #fefefe;
  margin: 15% auto; /* 15% from the top and centered */
  padding: 20px;
  border: 1px solid #888;
  width: 80%; /* Could be more or less, depending on screen size */
}

/* The Close Button */
.close {
  color: #aaa;
  float: right;
  font-size: 28px;
  font-weight: bold;
}

.close:hover,
.close:focus {
  color: black;
  text-decoration: none;
  cursor: pointer;
}
</style>
