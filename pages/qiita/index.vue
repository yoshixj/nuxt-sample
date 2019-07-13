<template lang="html">
  <div class="">
    <h3>Nuxt.js のタグをつけられた投稿の一覧</h3>
    <ul>
      <li v-for="item in items" :key="item.id">
        <h4>
          <span>{{item.title}}</span>
          <!-- <small> by {{item.user.id}}</small> -->
          <small>
            <span>by </span>
            <nuxt-link :to="`/users/${item.user.id}`">
              {{item.user.id}}
            </nuxt-link>
          </small>
        </h4>
        <div class="">
          {{ item.body.slice(0, 130) }}
        </div>
        <p><a :href="item.url">{{item.url}}</a></p>
      </li>
    </ul>

  </div>
</template>

<script>
export default {
  async asyncData({ app }) {
    const items = await app.$axios.$get('https://qiita.com/api/v2/items?query=tag:nuxt.js')
    return {
      items
    }
  }
}
</script>

<style lang="css">
</style>
