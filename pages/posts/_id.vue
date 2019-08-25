<template lang="html">
  <div class="container">
    <article>
      <h1 class="title">{{post.title}}</h1>
      <p>{{post.content}}</p>
    </article>
    <aside>
      <h3>Posts you might not enjoi</h3>
      <ul>
        <!-- Computed method below -->
        <li v-for="related in relatedPosts">
          <!-- Use nuxt-link instead of <a> tags, which cause the browser to reload, this is faster with no reload -->
          <!-- <a :href="`/posts/${related.id}`">
            {{related.title}}</a> -->

          <!-- Link option 1: pass an object -->
          <nuxt-link :to="{
            name: 'posts-id',
            params: { id: related.id }
            }">
            {{related.title}}
          </nuxt-link>

          <!-- Link option 2: pass route template literal -->
          <!-- <nuxt-link :to="`/posts/${related.id}`">
            {{related.title}}
          </nuxt-link> -->
        </li>
      </ul>
    </aside>
  </div>
</template>

<script>
export default {
  // The head method sets <head><title> to the post title, and all the meta data as well (here set for Twitter)
  head () {
    return {
      title: this.post.title,
      meta: [
        { name: 'twitter:title', content: this.post.title},
        { name: 'twitter:description', content: this.post.content},
        { name: 'twitter:image', content: 'https://i.imgur.com/UYP2umJ.png'},
        { name: 'twitter:card', content: 'summary_large_image'}
      ]
    }
  },
  data () {
    // console.log(this.$route);
    return {
      // id is pages/posts/_id.vue route which
      // dynamically resolves to URL param, e.g.,
      // localhost:3000/posts/shimp, so 'shimp' it is!
      // In other words, the $route obj has
      // param.id = 'shimp' the URL parameter
      id: this.$route.params.id,
      // posts: [] // now in Vuex store posts.js
    }
  },
  computed: {
    post() {
      // this.$store.state.posts.all from Vuex posts.js
      // this.id is the data id prop above
      return this.$store.state.posts.all.find(post => post.id === this.id)
    },
    // Return any posts except current param post
    relatedPosts() {
      return this.$store.state.posts.all.filter(post => post.id !== this.id)
    }
  }
}
</script>

<style lang="css" scoped>
  .container {
    display: flex;
    justify-content: space-between;
    line-height: 1.5;
  }
  article * {
    margin-bottom: 1rem;
  }
  aside {
    min-width: 280px;
    max-width: 280px;
    padding-left: 2rem;
  }
  .title {
    font-size: 2rem;
  }
</style>
