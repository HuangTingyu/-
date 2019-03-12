<template>
    <div>
        <router-link to="/" class="header-abs" v-show="showAbs">
            <div class="iconfont header-abs-back-icon">&#xe624;</div>
        </router-link>
        <div class="header-fixed" v-show="!showAbs" :style="opacityStyle">
            <router-link to="/">
                <span class="iconfont header-fixed-back">&#xe624;</span>
            </router-link>
            <span class="header-desc">城市选择</span>
        </div>
    </div>
</template>

<script>
export default {
  name: 'DetailHeader',
  data () {
    return {
      showAbs: true,
      opacityStyle: {
        opacity: 0
      }
    }
  },
  methods: {
    handleScroll () {
      const top = document.documentElement.scrollTop
      if (top > 60) {
        let opacity = top / 140
        opacity = opacity > 1 ? 1 : opacity
        this.opacityStyle = {opacity}
        this.showAbs = false
      } else {
        this.showAbs = true
      }
    }
  },
  activated () {
    window.addEventListener('scroll', this.handleScroll)
  },
  deactivated () {
    window.removeEventListener('scroll', this.handleScroll)
  }
}
</script>

<style lang="stylus" scoped>
@import '~styles/varibles.styl'
.header-abs
    position:absolute
    left:.2rem
    top:.2rem
    width:.8rem
    height:.8rem
    border-radius:.4rem
    text-align: center
    line-height: .8rem
    background: rgba(0,0,0,.8)
    .header-abs-back-icon
        color:#fff
        font-size:.4rem
.header-fixed
    z-index: 10
    position: fixed;
    top:0
    left:0
    right:0
    background-color: $bgColor;
    text-align: center;
    height:$headerHeight;
    line-height:$headerHeight;
    .header-desc
        position:fixed;
        left:50%;
        margin-left:-1rem;
        width:2rem;
        color:#fff;
        font-size:.32rem;
    .header-fixed-back
        position:absolute;
        top:0;
        left:0;
        width:.64rem;
        font-size:.4rem;
        text-align: center
        color:#fff;
</style>
