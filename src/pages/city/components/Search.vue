<template>
    <div>
        <div class="search">
            <input v-model="keyword" type="text" class="search-input" placeholder="输入城市名或拼音">
        </div>
        <!-- ----------------
        search-content里的v-show，用于解除bug:
        搜索框里没内容时的霸屏
        --------------------------->
        <div class="search-content" ref="search" v-show = "keyword">
            <ul>
                <li class="search-item border-bottom" v-for="item of list" :key="item.id"
                    @click="handleCityClick(item.name)">
                    {{item.name}}</li>
               <!---------------
               v-show用于解除bug:
               没有找到匹配数据
               ------------------>
                <li class="search-item border-bottom" v-show = "hasNoData">没有找到匹配数据</li>
            </ul>
        </div>
    </div>
</template>

<script>
import Bscroll from 'better-scroll'
import { mapMutations } from 'vuex'
export default {
  name: 'CitySearch',
  props: {
    cities: Object
  },
  methods: {
    // Vuex的使用
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
  computed: {
    hasNoData () {
      return !this.list.length
    }
  },
  data () {
    return {
      keyword: '',
      list: [],
      timer: null
    }
  },
  watch: {
    // 以下是监听keyword的改变部分
    keyword () {
      // 首先，加定时器节流
      if (this.timer) {
        clearTimeout(this.timer)
      }
      // 此处为了解决bug,搜索框清空,页面仍显示搜索内容
      if (!this.keyword) {
        this.list = []
        return
      }
      this.timer = setTimeout(() => {
        const result = []
        // 循环cities
        for (let i in this.cities) {
          // forEach基本用法，遍历数组，把数组元素代到回调函数中
          // forEach遍历键值对如'A'，数组里面的值
          this.cities[i].forEach((value) => {
            // indexOf返回字符在字符串中第一次出现的索引位置
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
    // 此处解决搜索内容过多，无法滚动的bug
    this.scroll = new Bscroll(this.$refs.search)
  }
}
</script>

<style lang="stylus" scoped>
@import '~styles/varibles.styl'
.search
    height:.72rem;
    padding:0 .1rem;
    background: $bgColor;
    .search-input
        box-sizing :border-box;
        width:100%;
        padding:0 .1rem;
        height:.62rem;
        line-height:.62rem;
        text-align: center;
        border-radius:.06rem;
.search-content
    z-index:1
    overflow:hidden
    position:absolute
    top:1.58rem
    left:0
    right:0
    bottom:0
    background: #eee
    .search-item
        line-height:0.62rem
        padding:.2rem
        color:#666
        background: #fff
</style>
