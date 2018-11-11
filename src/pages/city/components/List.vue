<template>
  <div class="list" ref="wrapper">
    <div>
         <div class="area">
      <div class="title border-topbottom">当前城市</div>
      <div class="button-list">
        <div class="button-warper">
          <div class="button">{{this.currentCity}}</div>
        </div>
      </div>
    </div>
  <div class="area">
      <div class="title border-topbottom">热门城市</div>
      <div class="button-list">
        <div class="button-warper" v-for="item of hotCities" @click="handleCityClick(item.name)" :key="item.id">
          <div class="button">{{item.name}}</div>
        </div>
      </div>
    </div>
    <div class="area" v-for="(item,key) of cities" :key="key" :ref="key">
      <div class="title border-topbottom">{{key}}</div>
      <div class="item-list">
        <div class="item  border-bottom" v-for='innerItem of item'  @click="handleCityClick(innerItem.name)" :key="innerItem.id">{{innerItem.name}}</div>
      </div>
    </div>
    </div>
  </div>
</template>

<script>
import Bscroll from 'better-scroll'
import {mapState, mapMutations} from 'vuex'
export default {
  name: 'CityList',
  props: {
    cities: Object,
    hotCities: Array,
    letter: String
  },
  computed: {
    ...mapState({
      currentCity: 'city'
    })
  },
  methods: {
    handleCityClick (city) {
      this.changeCity(city)
      this.$router.push('/')
    },
    ...mapMutations(['changeCity'])
  },
  watch: {
    letter () {
      if (this.letter) {
        const ele = this.$refs[this.letter][0]
        this.scroll.scrollToElement(ele)
      }
    }
  },
  mounted () {
    this.scroll = new Bscroll(this.$refs.wrapper)
  }
}

</script>
<style lang='stylus' scoped>
 @import '~styles/varibles.styl'
  .border-topbottom
    &:before
      border-color :#ccc
    &:after
      border-color :#ccc
  border-bottom
    &:before
      border-color :#ccc
  .list
    position: absolute
    top:1.55rem
    left :0
    bottom :0
    right :0
    overflow :hidden
    .title
      line-height : .44rem
      padding-left : .2rem
      font-size:.26rem
      background :#eee
      color :#666
    .button-list
      overflow: hidden
      padding : .1rem .4rem .1rem .1rem
      .button-warper
        float: left
        width :33.33%
        .button
          text-align :center
          margin :.1rem
          padding: .1rem 0
          border:.02rem solid #ccc
          border-radius : .06rem
    .item-list
      .item
        line-height :.54rem
        color :#666
        padding:.1rem .2rem
</style>
