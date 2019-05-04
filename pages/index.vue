<template lang="pug">
  section.container
    div
      h1
        | Posts of vue.js
      ul
        li.post(v-for="item in items" :key="item.id")
          h2
            span {{ item.title }}
            span.posted
              | posted by
              nuxt-link(:to="`/users/${item.user.id}`")
                | {{ item.user.id }}
          div {{ item.body.slice(0, 130) }}...
          p
            a(:href="item.url") {{ item.url }}
</template>

<script>
export default {
  async asyncData({ app }) {
    const items = await app.$axios.$get('https://qiita.com/api/v2/items?query=tag:vue.js')
    return { items }
  }
}
</script>

<style>
.container {
  min-height: 100vh;
  padding: 20px;
}

h1 {
  font-size: 24px;
  border-bottom: solid 1px #eeeeee;
  margin-bottom: 25px;
}

li.post {
  margin-bottom: 15px;
}

h2 span {
  font-size: 20px;
}

h2 span.posted {
  margin-left: 10px;
  font-size: 16px;
}

h2 span.posted a {
  margin-left: 5px;
}

</style>
