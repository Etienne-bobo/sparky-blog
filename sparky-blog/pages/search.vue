<template>
  <div>
    <Search :query="text" />
    <div>
      <Posts :posts="posts" />
    </div>
  </div>
</template>

<script>
import searchPostsQuery from '~/apollo/queries/post/search'
import Search from '~/components/Search'
import Posts from '~/components/Posts'
export default {
  components: {
    Search,
    Posts,
  },
  data() {
    return {
      posts: [],
      text: '',
    }
  },

  beforeMount() {
    this.text = this.$route.query.text ?? ''
  },

  apollo: {
    posts: {
      prefetch: true,
      query: searchPostsQuery,
      variables() {
        return { text: this.$route.query.text ?? '' }
      },
      // error(data) {
      //   console.log(data)
      // },
      // result({ data, loading, networkStatus }) {
      //   console.log(data)
      // },
    },
  },
}
</script>

<style></style>
