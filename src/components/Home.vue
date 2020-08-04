<template>
  <section class="section">
    <div class="columns">
      <div class="column is-6 is-offset-3">
        <h1 class="title">Latest Posts</h1>

        <h3
          v-for="post in allPosts"
          :key="post.id"
          class="title is-5">
          <router-link :to="post.idea">
            {{ post.created }}
          </router-link>
        </h3>
      </div>
    </div>
  </section>
</template>

<script>
import { ALL_USERS_QUERY } from '@/graphql'

export default {
  name: 'Home',
  data () {
    return {
      allPosts: []
    }
  },
  async mounted () {
    this.loading = true
    const users = await this.$apollo.query({ query: ALL_USERS_QUERY })
    this.allPosts = users.data.ideas
    console.log(this.allPosts)
    this.loading = false
  }
  // apollo: {
  //   // fetch all posts
  //   allPosts: {
  //     query: ALL_POSTS_QUERY
  //   }
  // }
}
</script>
