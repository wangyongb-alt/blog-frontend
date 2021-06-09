<template>
  <Layout>
      <!-- Page Header-->
    <header class="masthead" style="background-image: url('/img/home-bg.jpg')">
        <div class="container position-relative px-4 px-lg-5">
            <div class="row gx-4 gx-lg-5 justify-content-center">
                <div class="col-md-10 col-lg-8 col-xl-7">
                    <div class="site-heading">
                        <h1>Clean Blog</h1>
                        <span class="subheading">A Blog Theme by Start Bootstrap</span>
                    </div>
                </div>
            </div>
        </div>
    </header>
    <!-- Main Content-->
    <div class="container px-4 px-lg-5">
        <div class="row gx-4 gx-lg-5 justify-content-center">
            <div class="col-md-10 col-lg-8 col-xl-7">
                <!-- Post preview-->
                <div class="post-preview" v-for="(item, index) in $page.posts.edges" :key="index">
                    <g-link :to="`/post/${item.node.id}`">
                        <h2 class="post-title">{{item.node.title}}</h2>
                    </g-link>
                    <p class="post-meta">
                        Posted publishTime
                        {{item.node.created_at}}
                    </p>
                    <p >
                        <span v-for="tag in item.node.tags" :key="tag.id">
                            <a href="" >{{tag.title}}</a>&nbsp;&nbsp;
                        </span>
                    </p>
                    <hr class="my-4" />
                </div>
                <!-- Pager-->
                <!-- <div class="d-flex justify-content-end mb-4"><a class="btn btn-primary text-uppercase" href="#!">Older Posts →</a></div> -->
                <Pager :info="$page.posts.pageInfo"/>
            </div>
        </div>
    </div>
  </Layout>
</template>

<page-query>
query ($page: Int) {
  posts: allStrapiPost(perPage: 1, page: $page) @paginate {
    pageInfo {
      totalPages
      currentPage
    }
    edges {
      node {
        id
        title
        created_at
        tags {
          id
          title
        }
      }
    }
  }
}
</page-query>

<script>
import { Pager } from 'gridsome'

export default {
  name: "HomePage",
  components: {
    Pager
  },
  metaInfo: {
    title: 'Hello, world!'
  }
}
</script>

<style>

</style>
