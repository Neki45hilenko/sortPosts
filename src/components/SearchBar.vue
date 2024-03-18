<template>
  <div class="input-group mb-3 d-flex align-items-center">
    <div class="input-group-text">
      <img
        src="../assets/find-svgrepo-com.svg"
        alt="searching"
        height="24.67px"
      />
    </div>
    <input
      type="text"
      class="form-control"
      v-model="query"
      placeholder="Search posts by author..."
      @input="validateInput"
    />
  </div>
</template>

<script setup>
import { inject, ref } from "vue";

const query = inject("query");
const inputValue = ref("");

const validateInput = (event) => {
  const regex = /^[a-zA-Zа-яА-Я]*$/u;
  const input = event.target.value;

  if (regex.test(input)) {
    inputValue.value = input;
    query.value = input;
  } else {
    inputValue.value = inputValue.value.slice(0, -1);
    query.value = inputValue.value;
  }
};
</script>

<style lang="scss" scoped>
.input-group-text {
  background-color: transparent;
  border-right: none;
  border-radius: 0.25rem 0 0 0.25rem;
}
</style>
