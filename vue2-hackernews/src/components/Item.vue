<template>
  <li class="news-item">
    <!-- 评分 -->
    <span class="score">{{ item.score }}</span>
    <!-- 标题&网址 -->
    <span class="title">
      <template v-if="item.url">
        <a :href="item.url" target="_blank">{{ item.title }}</a>
        <span class="host">({{ item.url | host }})</span>
      </template>
      <template v-else>
        <router-link :to="'/item/' + item.id">{{ item.title }}</router-link>
      </template>
    </span>
    <br>
    <span class="meta">
      <!-- 作者 -->
      <span class="by" v-if="item.type !== 'job'">
        by <router-link :to="'/user/' + item.by">{{ item.by }}</router-link>
      </span>
      <!-- 时间 -->
      <span class="time">
        {{item.time | timeAgo }} ago
      </span>
      <!-- 评论 -->
      <span class="comments-link" v-if="item.type !== 'job'">
        | <router-link :to="'/item/' + item.id">{{ item.descendants }} comments</router-link>
      </span>
    </span>
    <span class="label" v-if="item.type !== 'story'">{{ item.type }}</span>
  </li>
</template>

<script>
export default {
  name:'news-item',
  props:['item'],
  serverCacheKey: props => {
    return `${props.item.id}::${props.item.__lastUpdated}`
  }
}
</script>

<style lang="stylus">
.news-item
  background-color #fff
  padding 20px 30px 20px 80px
  border-bottom 1px solid #eee
  position relative
  line-height 20px
  .score
    color #ff6600
    font-size 1.1em
    font-weight 700
    position absolute
    top 50%
    left 0
    width 80px
    text-align center
    margin-top -10px
  .meta, .host
    font-size .85em
    color #999
    a
      color #999
      text-decoration underline
      &:hover
        color #ff6600
</style>
