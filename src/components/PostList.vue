<template>
  <div class="row">
    <div
      class="col-lg-4 col-md-6 col-sm-12"
      v-for="post in filteredPosts"
      :key="post.id"
    >
      <PostItem :post="post" />
    </div>
  </div>
</template>

<script setup>
import { inject, computed } from "vue";
import PostItem from "./PostItem.vue";

const props = defineProps({
  posts: {
    type: Array,
    required: true,
  },
});

const query = inject("query");

const filteredPosts = computed(() => {
  return props.posts.filter((post) => {
    const user = post.user || {};
    const name = user.name || "";
    return name.toLowerCase().includes(query.value.toLowerCase());
  });
});
</script>
