<template>
 <Layout>
    <!-- Page Header-->
    <header class="masthead" style="background-image: url('/img/home-bg.jpg')">
        <div class="container position-relative px-4 px-lg-5">
            <div class="row gx-4 gx-lg-5 justify-content-center">
                <div class="col-md-10 col-lg-8 col-xl-7">
                    <div class="site-heading">
                        <h1>{{$page.general.edges[0].node.title}}</h1>
                        <span class="subheading">{{$page.general.edges[0].node.subTitle}}</span>
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
                <div class="post-preview" v-for="edge in $page.posts.edges" :key="edge.node.id">
                    <g-link :to="'/post/' + edge.node.id">
                        <h2 class="post-title">{{edge.node.title}}</h2>
                        <!-- <h3 class="post-subtitle">Problems look mighty small from 150 miles up</h3> -->
                    </g-link>
                    <!-- <p class="post-meta">
                        Posted by
                        <a href="#!">{{edge.node.created_by.firstname + edge.node.created_by.lastname}}</a>
                        on {{edge.node.created_at}}
                    </p> -->
                    <p>
                        <g-link :to="'/tag/' + tag.id" v-for="tag in edge.node.tags" :key="tag.id">{{tag.title}}</g-link>
                    </p>
                </div>
                <!-- Divider-->
                <hr class="my-4" />
                <pager :info="$page.posts.pageInfo"/>
                <!-- Pager-->
                <!-- <div class="d-flex justify-content-end mb-4"><a class="btn btn-primary text-uppercase" href="#!">Older Posts →</a></div> -->
            </div>
        </div>
    </div>
 </Layout>
</template>

<page-query>
query($page: Int) {
  	posts: allStrapiPost(perPage: 2, page: $page) @paginate {
      pageInfo {
          totalPages
          currentPage
      }
      edges {
        node {
          id
          title
          tags {
              id
              title
          }
          created_at
        }
      }
    }
    general: allStrapiGeneral {
      edges {
        node {
          id
          title
          subTitle
        }
      }
    }
  }
</page-query>
<script>
import { Pager } from 'gridsome'
export default {
  name: 'HomePage',
  metaInfo: {
    title: 'Hello, world!'
  },
  components: {
      Pager
  }
}
</script>
