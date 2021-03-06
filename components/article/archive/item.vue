<template>
  <div class="article-list-item">
    <div class="item-content">
      <div class="item-thumb">
        <router-link :to="`/article/${item.id}`">
          <img class="item-thumb-img" :src="buildThumb(item.thumb)">
        </router-link>
      </div>
      <div class="item-body">
        <h4 class="item-title">
          <router-link :to="`/article/${item.id}`">{{ item.title }}</router-link>
        </h4>
        <p class="item-description" style="-webkit-box-orient: vertical;">{{ item.description }}</p>
        <div class="item-meta">
          <span class="date">
            <i class="iconfont icon-clock"></i>
            <span>{{ item.create_time | toYMD }}</span>
          </span>
          <span class="views">
            <i class="iconfont icon-eye"></i>
            <span>{{ item.meta.views || 0 }}</span>
          </span>
          <span class="comment">
            <i class="iconfont icon-comment"></i>
            <span>{{ item.comment.length || 0 }}</span>
          </span>
          <span class="category">
            <i class="iconfont icon-list"></i>
            <span v-if="!item.category.length">未分类</span>
            <router-link :to="`/category/${category.slug}`" 
                         v-for="category in item.category">{{ category.name }}</router-link>
          </span>
          <span class="tag">
            <i class="iconfont icon-tag"></i>
            <span v-if="!item.tag.length">无</span>
            <router-link :to="`/tag/${tag.slug}`" v-for="tag in item.tag">{{ tag.name }}</router-link>
          </span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'article-list-item',
    props: {
      item: Object
    },
    methods: {
      buildThumb(thumb) {
        if (!thumb) return '/images/thumb-article.jpg'
        return `${thumb}?imageView2/1/w/350/h/238/interlace/0/q/100|watermark/2/text/U3VybW9uLm1l/font/Y2FuZGFyYQ==/fontsize/456/fill/I0ZGRkZGRg==/dissolve/20/gravity/SouthWest/dx/15/dy/7`
      }
    }
  }
</script>

<style lang="scss">
  @import '~assets/sass/variables';
  @import '~assets/sass/mixins';
  .article-list-item {
    margin-bottom: 1em;
    background-color: $module-bg;

    &:last-child {
      margin: 0;
    }

    &:hover {
      background-color: $module-hover-bg;
    }

    > .item-content {
      display: block;
      overflow: hidden;
      height: 9.5em;
      padding: .5em;

      > .item-thumb {
        float: left;
        width: 12em;
        height: 8.5em;
        overflow: hidden;

        .item-thumb-img {
          min-width: 100%;
          width: calc(100% + .5em);
          max-width: calc(100% + .5em);
          height: auto;
          min-height: 8.5em;
          border-color: transparent;
          background-color: #c0c0c0;
          @include css3-prefix(opacity, 1);
          @include css3-prefix(filter, grayscale(0.3));
          @include css3-prefix(transform, translateX(0));

          &:hover {
            @include css3-prefix(opacity, .95);
            @include css3-prefix(filter, grayscale(0));
            @include css3-prefix(transform, translateX(-.5em));
          }
        }
      }

      > .item-body {
        float: right;
        width: 28.5em;
        height: 8.5em;

        > .item-title {
          font-size: 1em;
          font-weight: bold;
          color: #333;
          margin-top: .2em;
          margin-bottom: .5em;
          overflow: hidden;
          text-overflow: ellipsis;
          white-space: nowrap;

          > a {
            margin-left: 0;

            &:hover {
              display: inline-block;
              text-decoration: underline;
              margin-left: .5em;
            }
          }
        }

        > .item-description {
          font-size: .9em;
          margin: 0;
          margin-bottom: 0.3em;
          height: 5em;
          line-height: 1.8em;
          overflow: hidden;
          text-overflow: ellipsis;
          @include clamp(3);
        }

        > .item-meta {
          font-size: .9em;
          height: 2em;
          line-height: 2em;
          display: block;
          white-space: nowrap;
          overflow: hidden;
          text-overflow: ellipsis;
          word-wrap: normal;

          > .date,
          > .views,
          > .comment,
          > .tag,
          > .category {
            // display: inline-block;
            // float: left;
            margin-right: 1em;

            > .iconfont {
              font-size: 1em;
              margin-right: .4em;
            }
          }

          > .tag,
          > .category {

            a {
              text-transform: capitalize;
              margin-right: .5em;
            }
          }

          > .tag {
            margin-right: 0;
          }
        }
      }
    }
  }
</style>
