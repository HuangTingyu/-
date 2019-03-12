<template>
    <div class="list" ref="wrapper">
        <div>
            <div class="area">
                <div class="title border-topbottom">当前城市</div>
                <div class="button-list">
                    <div class="button-wrapper">
                        <!----------
                        Vuex的使用
                        此处，打通home/Header组件
                        ------------->
                        <div class="button">{{this.currentCity}}</div>
                    </div>
                </div>
            </div>
            <div class="area">
                <div class="title border-topbottom">热门城市</div>
                <div class="button-list">
                    <!-----------
                    handleCityClick函数实现Vuex三部曲
                    Vuex三部曲：actions,mutations,state
                    ----------->
                    <div class="button-wrapper" v-for="item of hot" :key="item.id " @click="handleCityClick(item.name)">
                        <div class="button">{{item.name}}</div>
                    </div>
                </div>
            </div>
            <div class="area" v-for="(item,key) of cities" :key="key" :ref="key">
                <div class="title border-topbottom" >{{key}}</div>
                <!----------------------->
                <!-- 列表部分添加Vuex函数handleCityClick-->
                <div class="item-list">
                    <div class="item border-bottom" v-for="innerItem of item" :key="innerItem.id" @click="handleCityClick(innerItem.name)">{{innerItem.name}}</div>
                </div>
            </div>
        </div>
    </div>

</template>

<script>
import Bscroll from 'better-scroll'
import { mapState, mapMutations } from 'vuex'
export default {
  name: 'CityList',
  props: {
    hot: Array,
    cities: Object,
    letter: String
  },
  computed: {
    ...mapState({
      currentCity: 'city'
    })
  },
  methods: {
    // ！！！！！！！！！！！！！！！！！！！！！！！！
    // Vuex三部曲的实现
    handleCityClick (city) {
      // 方法I：表示我要派发一个changeCity的actions,并把city传过去
      // this.$store.dispatch('changeCity', city)
      // ------------------------------------
      // 方法II：没有异步操作，没必要调用actions
      // commit方法直接调用mutation
      // this.$store.commit('changeCity', city) （1）
      // 以下是（1）经过mapMutations的转换
      this.changeCity(city)
      this.$router.push('/')
    },
    ...mapMutations(['changeCity'])
  },
  watch: {
    letter () {
      if (this.letter) {
        const element = this.$refs[this.letter][0]
        // console.log(element)
        this.scroll.scrollToElement(element)
      }
      // console.log(this.letter)
    }
  },
  mounted () {
    this.scroll = new Bscroll(this.$refs.wrapper)
  }
}
</script>

<style lang="stylus" scoped>
@import '~styles/varibles.styl'
.border-topbottom
    &:before
        border-color:#ccc
    &:after
        border-color:#ccc
.border-bottom
    &:before
        border-color:#ccc
.list
    position:absolute;
    top:1.58rem;
    left:0;
    right:0;
    bottom:0;
    overflow:hidden;
    .title
        color:#666;
        line-height: .54rem;
        background: #eee;
        padding-left :.2rem;
        font-size:.26rem;
    .button-list
        overflow:hidden
        padding.1rem .6rem .1rem .1rem;
        .button-wrapper
            float:left;
            width:33.33%;
            .button
                margin:.1rem .1rem;
                border:.02rem solid #ccc;
                border-radius:.06rem;
                padding:.1rem 0;
                text-align: center;
    .item-list
        .item
            padding-left:.2rem;
            line-height:.54rem;
</style>
