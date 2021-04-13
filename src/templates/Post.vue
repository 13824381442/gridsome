<template>
  <Layout>
    <div class='post-content'>
      <img class='post-img' :src="imageUrl + post.image.url">
      <div class='content-info'>
        <h1>{{post.nickname}}</h1>
        <h2>{{post.name}}</h2>
        <h2>{{post.type}}</h2>
        <h3>简介：</h3>
        <div class='info-text' v-html="post.content"></div>
      </div>
    </div>
  </Layout>
</template>

<page-query>
  query ($id: ID!) {
    post: strapiPost (id: $id) {
      id
      name
      type
      nickname
      content
      image {
        url
      }
    }
  }
</page-query> 

<script>
export default {
  name: 'Post',
  metaInfo: {
    title: 'Post'
  },
  computed: {
    post () {
      console.log(this.$page.post)
      return this.$page.post
    }
  }
}
</script>

<style>
  .post-content {
    padding: 100px 300px;
    display: flex;
  }
  .post-img {
    width: 400px;
    height: 250px;
  }
  .content-info {
    margin-left: 50px;
  }
  h1 {
    margin-top: 0px;
  }
</style>