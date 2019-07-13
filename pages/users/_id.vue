<template>
  <section>
    <div>
      <h3>{{user.id}}</h3>
      <img :src="user.profile_image_url" width="120">
      <p>
        <nuxt-link to="/qiit  a/">
          <small><b>トップへ戻る</b></small>
        </nuxt-link>
      </p>
      <h3>{{user.id}}さんの投稿一覧</h3>
    </div>
    <ul>
      <li v-for="item in items" :key="item.id">
        <h4>
          <span>{{item.title}}</span>
        </h4>
        <div class="">
          {{item.body.slice(0, 130)}}
        </div>
      </li>
    </ul>
  </section>
</template>

<script>
export default {
  data() {
    return {
      userId: this.$route.params.id
    }
  },
  head() {
    return {
      title: `ユーザーページ ${this.user.id}`
    }
  },
  async asyncData({route, app}) {
    const user = await app.$axios.$get(`https://qiita.com/api/v2/users/${route.params.id}`)
    const items = await app.$axios.$get(`https://qiita.com/api/v2/items?query=user:${route.params.id}`)
    return { user, items}
  }
}
</script>
