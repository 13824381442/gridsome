<template>
  <Layout>
    <div class='index'>
      <div class="posts-content">
        <div class="content-item" 
          v-for='(post) in posts' 
          :key='post.id'
          @mouseover="move(post.id)" 
          @mouseleave="move(-1)">
          <g-link class="item" :class='id === post.id ? "item-bg" : ""' :to='"/post/" + post.id'>
            <img :src="imageUrl + post.image.url" class='img-left'>
            <div class='item-info'>
              <h1>{{post.nickname}}</h1>
              <h3>{{post.name}}</h3>
              <h3>{{post.type}}</h3>
              <div :class='id === post.id ? "content-active" : "content"'>{{post.content}}</div>
            </div>
          </g-link>
        </div>
      </div>
    </div>
  </Layout>
</template>

<page-query>
  query ($id: ID!) {
    tags: strapiTag (id: $id) {
    id
    title
    posts {
      id
      nickname
      name
      type
      content
      image {
        url
      }
    }
  }
  }
</page-query> 

<script>
export default {
  name: 'Posts',
  metaInfo: {
    title: 'Posts'
  },
  data () {
    return {
      id: -1
    }
  },
  computed: {
    posts () {
      return this.$page.tags.posts
    },
  },
  methods: {
    move (id) {
      this.id = id
      console.log(id)
    }
  }
}
</script>

<style>
.posts-content {
  padding: 0px 300px;
  margin-top: 100px;
  margin-bottom: 100px;
}
.content-item {
  margin-bottom: 30px;
}
h1 {
  margin-top: 0;
}
.item {
  width: 980px;
  margin: 0 auto;
  color: rgb(0, 0, 0);
  text-decoration: none;
  display: flex;
  justify-content: space-between;
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0px 0px 16px transparent;
  transition: all 0.2s linear;
}
.item-bg {
  box-shadow: 0px 0px 16px ;
}
.item-info {
  width: 300px;
  margin: 0 20px;
}
img {
  display: block;
  width: 600px;
  height: 350px;
}
.img-left {
  margin-right: 30px;
}
.content {
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 7;
  overflow: hidden;
  opacity: 0;
  transition: all 0.5s linear;
}
.content-active {
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 7;
  overflow: hidden;
  opacity: 1;
  transition: all 0.5s linear;
}
</style>
