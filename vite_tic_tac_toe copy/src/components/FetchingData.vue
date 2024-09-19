<template>
  <h1>Latest Vue Core Commits</h1>
  <div v-for="branch in branches" style="display: flex">
    <input
      id="branch"
      :value="branch"
      name="branch"
      type="radio"
      v-model="currentBranch"
    />
    <label :for="branch">{{ branch }}</label>
  </div>
  <h1>vuejs/vue@{{ currentBranch }}</h1>
  <ul v-for="{ sha, html_url, commit, author } in dataList">
    <li>
      <span
        ><a :href="html_url">
          {{ sha.slice(0, 7) }}
        </a> </span
      >-{{ convertLine(commit.message) }} by
      <a :href="author.html_url">
        {{ commit.author.name }}
      </a>
      at
      <b>
        {{ covertDate(commit.author.date) }}
      </b>
    </li>
  </ul>
</template>
<script setup>
import { ref, watchEffect } from "vue";
const branches = ["main", "v2-compat"];
const dataList = ref([]);
const url = "https://api.github.com/repos/vuejs/core/commits?per_page=3&sha=";
const currentBranch = ref("main");
watchEffect(async () => {
  const urlApi = `${url}${currentBranch.value}`;
  dataList.value = await (await fetch(urlApi)).json();
});

const covertDate = (date) => {
  return date.replace(/T|Z/g, " ");
};

const convertLine = (v) => {
  const newLine = v.indexOf("\n");
  return newLine > 0 ? v.slice(0, newLine) : v;
};
</script>
<style scoped>
a {
  color: red;
}
</style>
