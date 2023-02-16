<template>
  <div>Index page</div>
  <h1>Welcome to the homepage</h1>
  <NuxtLayout name="default"></NuxtLayout>

  <TheHeader />

  <div>
    <NuxtLink to="/detail">Detail page</NuxtLink> |
    <NuxtLink to="/user-admin/1">user-admin page</NuxtLink> |
    <NuxtLink to="/parent/child">parent child</NuxtLink>
  </div>

  <NuxtLayout name="custom"></NuxtLayout>

  <TheFooter />

  <TestMyButton />

  <LazyMountainsList v-if="show" />
  <button v-if="!show" @click="show = !show">Show List</button>

  <h2>{{ time }}</h2>

  <!-- 请求数据 -->
  <div v-if="data">
    <h2>{{ data.name }}</h2>
    <img :src="data.avatar_url" alt="avatar" />
    <ul>
      <li>Followers: {{ data.followers }}</li>
      <li>Following: {{ data.following }}</li>
      <li>Public Repos: {{ data.public_repos }}</li>
      <li>blog: <a target="blank" :href="data.blog">博客地址：</a></li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from 'vue'
const show = ref(false)
const time = ref(getTime())

// 请求数据
const url = 'https://api.github.com/users/xmllein'
// const { data, error } = useFetch(url)
const res = await useAsyncData('data', () =>
  fetch(url).then((res) => res.json())
)
const data = res.data
</script>
