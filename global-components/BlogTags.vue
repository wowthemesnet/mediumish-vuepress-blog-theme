<template>
<div class="row justify-content-center">

  <div class="blog-tags col-md-10 text-center mt-5">
     <h1 class="font-secondary mb-5 font-weight-bold"> {{$site.description}}</h1>
     <BlogTag v-for="tag in tags" :key="tag.name" :tag="tag" />
  </div>
  </div>
</template>

<script>
export default {
  props: ['tags'],
}
</script>

<style lang="stylus" scoped>
@import url('https://fonts.googleapis.com/css?family=Merriweather:400,400i,700&display=swap')
.blog-tags
  min-height:500px
.blog-tag
  border-radius:50px
  &:hover
    text-decoration:none
h1
  line-height:1.3
</style>
