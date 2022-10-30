// pages/[slug]/index.vue

<script setup>
const route = useRoute();
const slug = route.params.slug;
const ctx = useRuntimeConfig();

// const { data: article } = await useAsyncData("key",() => $fetch())
const { data: article } = await useFetch(`/blogs/${slug}`, {
  baseURL: ctx.baseURL,
  headers: {
    "X-MICROCMS-API-KEY": ctx.apiKey,
  },
  initialCache: false,
});
</script>

<template>
  <main class="main">
    <h1 class="title">{{ article.title }}</h1>
    <p class="publishedAt">
      <time :datetime="article.publishedAt" v-text="article.publishedAt" />
    </p>
    <div class="post" v-html="article.content" />
  </main>
</template>

<style lang="scss" scoped>
.main {
  width: 960px;
  margin: 0 auto;
}

.title {
  margin-bottom: 20px;
}

.publishedAt {
  margin-bottom: 40px;
}

:deep(.post) {
  > h2 {
    font-size: 24px;
    font-weight: bold;
    margin: 40px 0 16px;
    border-bottom: 1px solid #ddd;
  }

  > p {
    line-height: 1.8;
    letter-spacing: 0.2px;
  }
}
</style>
