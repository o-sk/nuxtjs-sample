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
import { mapGetters } from 'vuex'
import { awaitExpression } from 'babel-types';

export default {
  async asyncData({ store }) {
    if (store.getters['items'].length) {
      return
    }
    await store.dispatch('fetchItems')
  },
  computed: {
    ...mapGetters(["items"])
  }
}
</script>

<style lang="less">
.container {
  min-height: 100vh;
  padding: 20px;
}

h1 {
  font-size: 24px;
  border-bottom: solid 1px #eeeeee;
  margin-bottom: 25px;
}

.post {
  margin-bottom: 15px;

  h2 {
    span {
      font-size: 20px;

      &.posted {
        margin-left: 10px;
        font-size: 16px;

        a {
          margin-left: 5px;
        }
      }
    }
  }
}
</style>
