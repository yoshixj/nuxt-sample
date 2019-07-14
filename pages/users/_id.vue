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
import { mapGetters } from 'vuex'

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
  async asyncData({route, store, redirect}) {
    // const user = await app.$axios.$get(`https://qiita.com/api/v2/users/${route.params.id}`)
    // const items = await app.$axios.$get(`https://qiita.com/api/v2/items?query=user:${route.params.id}`)
    // return { user, items}
    if (store.getters['users'][route.params.id]) {
      return
    }
    try {
      await store.dispatch('fetchUserInfo', { id: route.params.id })
    } catch(e) {
      console.log(e);
      // redirect('/')
    }
  },
  computed: {
    user() {
      return this.users[this.$route.params.id]
    },
    items() {
      return this.userItems[this.$route.params.id]
    },
    ...mapGetters(['users', 'userItems'])
  }
}
</script>
