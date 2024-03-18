<template>
  <div class="card mb-4">
    <div class="card-body">
      <h5 class="card-title">{{ formattedTitle }}</h5>
      <p class="card-text">{{ formattedBody }}</p>
      <p class="card-text">
        <small class="text-muted"> {{ post.user?.name }} </small>
      </p>
    </div>
  </div>
</template>

<script setup>
import { computed } from "vue";

const props = defineProps({
  post: {
    type: Object,
    required: true,
  },
});

const formattedTitle = computed(() => {
  if (props.post.title) {
    return (
      props.post.title.charAt(0).toLocaleUpperCase() + props.post.title.slice(1)
    );
  }
  return "";
});

const formattedBody = computed(() => {
  if (props.post.body) {
    return (
      props.post.body.charAt(0).toLocaleUpperCase() + props.post.body.slice(1)
    );
  }
  return "";
});
</script>
