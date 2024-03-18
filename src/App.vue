<template>
  <div class="container">
    <h1 class="text-center my-4">Posts</h1>
    <SearchBar />
    <PostList :posts="posts" />
  </div>
</template>

<script setup>
import { ref, onMounted, provide } from "vue";
import SearchBar from "./components/SearchBar.vue";
import PostList from "./components/PostList.vue";

const posts = ref([]);
const users = ref([]);
const query = ref("");

provide("query", query);

onMounted(async () => {
  const responsePosts = await fetch(
    "https://jsonplaceholder.typicode.com/posts"
  );
  posts.value = await responsePosts.json();

  const responseUsers = await fetch(
    "https://jsonplaceholder.typicode.com/users"
  );
  users.value = await responseUsers.json();

  // Добавляем свойство user к каждому объекту post
  posts.value.forEach((post) => {
    const user = users.value.find((user) => user.id === post.userId);
    post.user = user;
  });
});
</script>
