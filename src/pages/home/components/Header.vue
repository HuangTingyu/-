<template>
    <div class="header">
        <div class="header-left">
            <div class="iconfont back-icon">&#xe624;</div>
        </div>
        <div class="header-input">
            <span class="iconfont">&#xe632;</span>
            输入城市/景点/游玩主题
        </div>
        <!--点击北京进行页面跳转-->
        <router-link to="/city">
            <div class="header-right">
                <!--------------
                此处：Vuex的使用
                ------------->
                <!--{{this.$store.state.city}}-->
                {{this.city}}
                <span class="iconfont arrow-icon">&#xe64a;</span>
            </div>
        </router-link>
    </div>
</template>
<script>
import { mapState } from 'vuex'
export default {
  name: 'HomeHeader',
  computed: {
    ...mapState(['city'])
  }
}
</script>
<style lang="stylus">
    @import '~styles/varibles.styl'
    /*  ~@  相当于前面的@ ，代表src目录*/
    .header
        display:flex
        line-height:.86rem
        background:$bgColor
        color:#fff
    .header-left
        width:.64rem
        float:left
        .back-icon
            text-align: center
            font-size:.4rem
            /*默认是50px,.4是20px*/
    .header-input
        flex:1
        height:.64rem
        line-height:.64rem
        margin-top:.12rem
        margin-left:.2rem
        background: #fff
        color:#ccc
        border-radius:.1rem
        padding-left:.2rem
    .header-right
        min-width:1.04rem
        padding:0 .1rem
        float:right
        text-align: center
        color:#fff
        .arrow-icon
            margin-left:-.04rem
            font-size:.24rem
</style>
