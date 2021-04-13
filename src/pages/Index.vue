<template>
  <Layout>
    <div class='index'>
      <div class="index-header"></div>
      <div class="index-content">
        <div class="content-item"
          v-for='(post, index) in posts' 
          :key='post.node.id' 
          @mouseover="move(post.node.id)" 
          @mouseleave="move(-1)">
          <g-link class="item" :class='id === post.node.id ? "item-bg" : ""' :to='"/post/" + post.node.id' v-if='index % 2 === 0'>
            <img :src="imageUrl + post.node.image.url" class='img-left'>
            <div class='item-info'>
              <h1>{{post.node.nickname}}</h1>
              <h3>{{post.node.name}}</h3>
              <h3>{{post.node.type}}</h3>
              <h3><span v-for="tag in post.node.tags" :key='tag.id'>{{tag.title}}</span></h3>
              <div :class='id === post.node.id ? "info-content-active" : "info-content"'>{{post.node.content}}</div>
            </div>
          </g-link>
          <g-link class="item" :class='id === post.node.id ? "item-bg" : ""' :to='"/post/" + post.node.id' v-else>
            <div class='item-info'>
              <h1>{{post.node.nickname}}</h1>
              <h3>{{post.node.name}}</h3>
              <h3>{{post.node.type}}</h3>
              <h3><span v-for="tag in post.node.tags" :key='tag.id'>{{tag.title}}</span></h3>
              <div :class='id === post.node.id ? "info-content-active" : "info-content"'>{{post.node.content}}</div>
            </div>
            <img :src="imageUrl + post.node.image.url" class='img-right'>
          </g-link>
        </div>
      </div>
      <div class='index-nav'>
        <div class='nav-content'>
          <g-link class='nav-item' 
            :to='"/posts/" + tag.node.id'
            :class='index < tags.length - 1 ? "nav-item-line" : ""' 
            v-for='(tag, index) in tags' 
            :key='tag.node.id'>
            {{tag.node.title}}
          </g-link>
        </div>
      </div>
    </div>
  </Layout>
</template>

<page-query>
  query {
    posts: allStrapiPost {
      edges {
        node {
          id
          name
          nickname
          type
          content
          image {
            url
          }
          tags {
            id
            title
          }
        }
      }
    }
    tags: allStrapiTag {
      edges {
        node {
          id
          title
        }
      }
    }
  }
</page-query> 

<script>
export default {
  name: 'home',
  metaInfo: {
    title: 'home'
  },
  data () {
    return {
      id: -1
    }
  },
  computed: {
    posts () {
      return this.$page.posts.edges
    },
    tags () {
      return this.$page.tags.edges
    }
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
span {
  margin-right: 10px;
}
.index-header {
  width: 100%;
  height: 520px;
  background-image: url('../../static/img/cover.jpg');
  background-size: cover;
}
.index-content {
  padding: 0 300px;
  margin-top: 30px;
  margin-bottom: 100px;
}
.content-item {
  margin-bottom: 30px;
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
h1 {
  margin-top: 0;
}
img {
  display: block;
  width: 600px;
  height: 350px;
  border-radius: 10px;
}
.item-info {
  width: 300px;
  margin: 0 20px;
}
.info-content {
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 4;
  overflow: hidden;
  opacity: 0;
  transition: all 0.5s linear;
}
.info-content-active {
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 4;
  overflow: hidden;
  opacity: 1;
  transition: all 0.5s linear;
}
.index-nav {
  margin-bottom: 50px;
  border-top: 0.5px solid rgb(175, 174, 174);
  border-bottom: 0.5px solid rgb(175, 174, 174);
}
.nav-content {
  padding: 0 300px;
  display: flex;
  justify-content: center;
}
.nav-item {
  height: 100px;
  width: 150px;
  font-size: 25px;
  line-height: 100px;
  color: black;
  text-align: center;
  text-decoration: none;
  transition: all 0.2s linear;
}
.nav-item:hover {
  background-color: rgb(180, 178, 178);
}
.nav-item-line {
  border-right: 0.5px solid rgb(175, 174, 174);
}
</style>
