<template>
<div>
  <div class="search">
    <input type="text" v-model='keyword' placeholder="输入城市内容或拼音" class="search-input">
  </div>
  <div class="search-content" ref="wrapper" v-show="keyword">
    <ul>
      <li class="search-item border-bottom" v-for='item of list' @click="handleCityClick(item.name)" :key='item.id'>{{item.name}}</li>
      <li v-show="hasNoData" class="search-item border-bottom">没有找到匹配的数据</li>
    </ul>
  </div>
</div>
</template>

<script>
import Bscroll from 'better-scroll'
export default {
  name: 'CitySearch',
  data () {
    return {
      keyword: '',
      list: [],
      timer: null
    }
  },
  methods: {
    handleCityClick (city) {
      this.$store.commit('changeCity', city)
      this.$router.push('/')
    }
  },
  props: { // 接受父组件传递过来的参数
    cities: Object
  },
  computed: { // 计算属性
    hasNoData () {
      return !this.list.length
    }
  },
  watch: {
    keyword () {
      if (this.timer) {
        clearTimeout(this.timer)
      }
      if (!this.keyword) {
        this.list = []
        return
      }
      this.timer = setTimeout(() => {
        const result = []
        for (let i in this.cities) {
          this.cities[i].forEach(value => {
            if (value.spell.indexOf(this.keyword) > -1 || value.name.indexOf(this.keyword) > -1) {
              result.push(value)
            }
          })
        }
        this.list = result
      }, 100)
    }
  },
  mounted () {
    this.scroll = new Bscroll(this.$refs.wrapper)
  }
}

</script>
<style lang='stylus' scoped>
 @import '~styles/varibles.styl'
  .search
    height :.7rem
    background : $bgColor
    padding: 0 .1rem
    .search-input
      height :.6rem
      line-height :.6rem
      width :100%
      text-align: center
      border-radius: .06rem
      color :#666
      padding: 0 .15rem
      box-sizing: border-box
  .search-content
    position: absolute
    top: 1.58rem
    left: 0
    right: 0
    bottom: 0
    overflow:hidden
    z-index: 1
    background: #eee
    .search-item
      line-height: .62rem
      padding-left: .2rem
      color: #666
      background :#fff
</style>
