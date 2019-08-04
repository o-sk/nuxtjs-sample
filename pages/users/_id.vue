<template lang="pug">
  section.container
    div
      h1 {{ user.id }}
      img(:src="user.profile_image_url" width="120" alt="")
      p {{ user.description || "No description" }}
      nuxt-link(to="/") トップに戻る

      h2 {{ user.id}}'s posts
      ul
        li.post(v-for="item in items" :key="item.id")
          h3 {{ item.title }}
          div {{ item.body.slice(0, 130) }}...
          p
            a(:href="item.url") {{ item.url }}

</template>

<script>
import { mapGetters } from 'vuex'
import { awaitExpression } from 'babel-types';

export default {
  head() {
    return {
      title: `${this.user.id}'s page`
    }
  },
  async asyncData({ route, store, redirect }) {
    if (store.getters['users'][route.params.id]) {
      return
    }
    try {
      await store.dispatch('fetchUserInfo', { id: route.params.id })
    } catch (e) {
      redirect("/")
    }
  },
  computed: {
    user() {
      return this.users[this.$route.params.id]
    },
    items() {
      return this.userItems[this.$route.params.id]
    },
    ...mapGetters(["users", "userItems"])
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
}
</style>
