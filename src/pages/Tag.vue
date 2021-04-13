<template>
  <Layout>
    <div class='tag-content'>
      <g-link :to='"/posts/" + tag.node.id' class='tag-item' v-for='tag in tags' :key='tag.node.id'>{{tag.node.title}}</g-link>
    </div>
  </Layout>
</template>

<page-query>
  query {
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
  name: 'Tag',
  metaInfo: {
    title: 'Tag'
  },
  computed: {
    tags () {
      return this.$page.tags.edges
    }
  }
}
</script>

<style>
  .tag-content {
    padding: 100px 300px;
    text-align: center;
  }
  .tag-item {
    display: block;
    margin: 0;
    height: 150px;
    line-height: 150px;
    font-size: 30px;
    color: black;
    transition: all 0.2s linear;
    text-decoration: none;
  }
  .tag-item:hover {
    background-color: rgba(0, 0, 0, 0.178);
    transition: all 0.2s linear;
  }
</style>