<template>
<div id="">

<div class="card-panel-content row" itemscope itemtype="http://schema.org/Blog">

<article
v-for="page in pages"
:key="page.key"
itemprop="blogPost"
class="ui-post entry col-md-4 card-container"
itemscope
itemtype="https://schema.org/BlogPosting"
>
  <meta itemprop="mainEntityOfPage" :content="page.path" />
  <div class="entry card h-100">
    <div class="card-header-image">
      <NavLink :link="page.path">
      <img :src="page.frontmatter.featuredimg"/>
      </NavLink>
    </div>

    <div class="card-inside">
      <div class="card-subheading">
        <div
        v-if="page.frontmatter.tags"
        class="ui-post-meta ui-post-tag"
        itemprop="keywords"
        >
        <router-link
        v-for="tag in resolvePostTags(page.frontmatter.tags)"
        :key="tag"
        :to="'/tag/' + tag"
        >
        {{ tag }}
        </router-link>
        </div>
      </div>
      <h2 class="heading" itemprop="name headline">
       <NavLink :link="page.path" class="heading">{{ page.title }}</NavLink>
      </h2>
      <p itemprop="description">{{ page.frontmatter.summary || page.summary }}</p>
    </div>
    <div class="meta-bottom mt-auto">


      <div v-if="$themeConfig.authors">
      <span
      v-for="author in $themeConfig.authors"
      :key="author.name"
      class="nav-item"
      >
      <div class="d-flex">
      <a class="profile-avatar">
      <img v-if="author.name === page.frontmatter.author" :src="($withBase)(author.avatar)" class="avatar-image" :alt="author.name">
      </a>
      <div class="meta">
      <div  v-if="author.name === page.frontmatter.author">
      <span class="username">{{author.name}}</span> &nbsp;
      </div>
      <div>
      </div>
      </div>
      </div>
      </span>
      </div>

      <div v-if="page.frontmatter.date" class="date"><time
      pubdate
      itemprop="datePublished"
      :datetime="page.frontmatter.date"
      >
      {{ resolvePostDate(page.frontmatter.date) }}
      </time> </div>



    </div>
  </div>
</article>
</div>

<component
:is="paginationComponent"
v-if="$pagination.length > 1 && paginationComponent"
></component>
</div>

</template>

<script>
/* global THEME_BLOG_PAGINATION_COMPONENT */

import Vue from 'vue'
import dayjs from 'dayjs'
import {
  Pagination,
  SimplePagination,
} from '@vuepress/plugin-blog/lib/client/components'

export default {


  data() {
    return {
      paginationComponent: null,
    }
  },

  computed: {
    pages() {
      return this.$pagination.pages
    },
  },

  created() {
    this.paginationComponent = this.getPaginationComponent()
  },

  methods: {
    getPaginationComponent() {
      const n = THEME_BLOG_PAGINATION_COMPONENT
      if (n === 'Pagination') {
        return Pagination
      }

      if (n === 'SimplePagination') {
        return SimplePagination
      }

      return Vue.component(n) || Pagination
    },

    resolvePostDate(date) {
      return dayjs(date).format(
        this.$themeConfig.dateFormat || 'ddd MMM DD YYYY'
      )
    },

    resolvePostTags(tags) {
      if (!tags || Array.isArray(tags)) return tags
      return [tags]
    },
  },
}
</script>

<style lang="stylus">
.pagination > li > a, .pagination > li > span
  border:0;
  border-bottom:1px solid #ddd
  font-size:15px
  font-weight:700
.pagination > li:last-child > a, .pagination > li:last-child > span, .pagination > li:first-child > a, .pagination > li:first-child > span
  border-radius:0
.pagination > li > a, .pagination > li > span
  color:inherit
  background:none
.pagination > .active > a, .pagination > .active > span, .pagination > .active > a:hover, .pagination > .active > span:hover, .pagination > .active > a:focus, .pagination > .active > span:focus
  background:none
  border-bottom: 1px solid
  color: $accentColor
.date
  margin-left: 50px;
  margin-top: -20px;
.username
  margin-top:-10px;
</style>
