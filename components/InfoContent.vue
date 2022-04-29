<template>
  <div class="main">
    <div class="content-header">
      <h1 class="header-title">{{ $page.title }}</h1>
    </div>
    <div v-if="categories.length || tags.length" class="content-tag">
      <div v-if="categories.length" class="inblock tag-list">
        <router-link
          v-for="(item, index) in categories"
          :key="index"
          :to="$pluginConfig.categoryIndexPageUrl + item + '/'"
          class="tag-text"
        >{{ item }}
        </router-link>
      </div>
      <span v-if="categories.length && tags.length" class="tag-space">/</span>
      <div v-if="tags.length" class="inblock tag-list">
        <router-link
          v-for="(item, index) in tags"
          :key="index"
          :to="$pluginConfig.tagIndexPageUrl + item + '/'"
          class="tag-text"
        >{{ item }}
        </router-link>
      </div>
    </div>
    <div class="player">
      <div class="info-content">
        <video
          style="aspect-ratio: 16 / 9; width: 100%"
          controls
          playsinline
          data-poster="poster.jpg"
        >
          <source
            :src="$frontmatter.src"
            type="video/mp4"
          />
        </video>
        <script src="https://cdn.plyr.io/3.6.12/plyr.js"></script>
      </div>
      <div class="info-right">
        <script type="application/javascript" data-idzone="4475804" src="https://a.realsrv.com/nativeads-v2.js" />
      </div>
    </div>
  </div>
</template>

<script>
import { getCategories, getTags } from '@theme/lib/util'
export default {
  name: 'InfoContent',
  computed: {
    categories() {
      return getCategories(this.$frontmatter)
    },
    tags() {
      return getTags(this.$frontmatter)
    },
    createTime() {
      return this.formatDate(this.$frontmatter.date)
    },
    lastUpdated() {
      return this.formatDate(this.$page.lastUpdated)
    },
    postTime() {
      return this.$themeConfig.postTime
    }
  },
  methods: {
    formatDate(date) {
      return (
        date && new Date(date).toLocaleString(this.$lang, this.postTime.options)
      )
    }
  }
}
</script>

<style lang="stylus" scoped>
.main
  padding 0
.content-header
  margin 0 auto
  width 100%
  max-width 84.75rem
  padding 0
  text-align left
  .header-title
    word-wrap: break-word;
    font-size 1.6rem
    color $blackColor
    font-weight bold
    text-shadow 0 1px 5px $shadowColor
    transition all .5s ease-in-out
    @media (prefers-color-scheme: dark)
      color $blackDarkColor
      text-shadow 0 1px 5px $shadowDarkColor
    @media print
      color $blackColor
      text-shadow none
.content-tag
  display flex
  flex-flow row wrap
  align-items center
  .tag-list
    :first-child
      background #3e3b3b
    padding 0 0 .5rem
    .tag-text
      display inline-block
      padding .2rem .5rem
      font-size 1.2rem
      color $accentColor
      transition all .5s ease-in-out
      @media (prefers-color-scheme: dark)
        color $accentDarkColor
  .tag-space
    color $blackColor
    transition color .5s ease-in-out
    @media (prefers-color-scheme: dark)
      color $blackDarkColor
.player
  display flex
  flex-wrap wrap
  .info-content
    box-sizing border-box
    padding-right 10px
    @media (max-width $phoneWidth)
      padding-right 0
      margin-bottom 10px
    flex 1 1 auto
    width 50vw
    @media (max-width $phoneWidth)
      width 100vw
    border-radius 1rem
    box-shadow 0px 0px 8px $shadowColor
    background $whiteColor
    transition all .5s ease-in-out
    @media (prefers-color-scheme: dark)
      box-shadow 0px 0px 8px $shadowDarkColor
      background $whiteDarkColor
    @media print
      box-shadow none
    .content-time
      padding 0 3rem 2rem
      text-align right
      @media print
        display none
      .time-text
        display block
        font-size .9rem
        color $textColor
        transition all .5s ease-in-out
        @media (prefers-color-scheme: dark)
          color $textDarkColor
  .info-right
    flex 1 1 auto
    width 15vw
    height 30vw
    overflow scroll
    @media (max-width $phoneWidth)
      flex 1 1 auto
      width 100vw
</style>
