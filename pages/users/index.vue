<template lang="pug">
  div
    p
      | /users/index.vue
</template>

<script>
export default {
  async mounted() {
    console.log(
      JSON.stringify(await
        this.$axios.$get('https://qiita.com/api/v2/items?query=tag:vue.js'), true, ' ')
    )
  }
}
</script>
