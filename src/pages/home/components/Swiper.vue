<template>
<div class="warpper">
    <swiper :options="swiperOption" v-if='showSwiper'>
        <swiper-slide v-for="item of list" :key="item.id">
            <img class="swiper-img" :src="item.imgUrl" alt="">
        </swiper-slide>
        <div class="swiper-pagination"  slot="pagination"></div>
    </swiper>
</div>
</template>

<script>
export default {
  name: 'HomeSwiper',
  props: {
    list: Array
  },
  data () {
    return {
      swiperOption: {
        pagination: '.swiper-pagination',
        loop: true,
        autoplay: 3000
      }
    }
  },
  computed: {
    showSwiper () {
      return this.list.length
    }
  }
}
</script>

<style lang="stylus" scoped>
.warpper >>> .swiper-pagination-bullet-active {
    background: #fff;
}

.warpper {
    width: 100%;
    height: 0;
    overflow: hidden;
    padding-bottom: 32%;
    .swiper-img {
        width: 100%;
        height: 100%
    }
}
</style>
