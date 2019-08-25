<template lang="html">
  <div class="container">
    <article>
      <h1 class="title">{{post.title}}</h1>
      <p>{{post.content}}</p>
    </article>
  </div>
</template>

<script>
export default {
  data () {
    console.log(this.$route);
    return {
      // id is pages/posts/_id.vue route which
      // dynamically resolves to URL param, e.g.,
      // localhost:3000/posts/shimp, so 'shimp' it is!
      // In other words, the $route obj has
      // param.id = 'shimp' the URL parameter
      id: this.$route.params.id,
      posts: [
        {
          id: 'balut',
          title: 'What is Balut?',
          content: 'Balut is not salad, which is delicious.'
        },
        {
          id: 'shimp',
          title: 'Who is Shimp?',
          content: 'Shimp is All Is One! Or NONE!'
        }
      ]
    }
  },
  computed: {
    post () {
      // this.param is the data id prop above
      return this.posts.find(post => post.id === this.id)
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
