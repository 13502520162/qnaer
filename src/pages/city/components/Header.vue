<template>
<div class="header">
  城市选择
 <router-link to="/">
   <div class="iconfont header-back">&#xe624;</div>
 </router-link>
</div>
</template>

<script>
export default {
  name: 'CityHeader'
}
</script>

<style lang='stylus' scoped>
 @import '~styles/varibles.styl'
  .header
    position: relative
    height :$headerHeigth
    line-height: $headerHeigth
    overflow :hidden
    text-align :center
    color :#fff
    background: $bgColor
    font-size : .3rem
    .header-back
      position: absolute
      top:0
      left:.12rem
      width :.4rem
      text-align :center
      font-size:.4rem
      color :#fff

</style>
