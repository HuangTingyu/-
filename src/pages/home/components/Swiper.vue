<template>
    <div class="wrapper">
        <!--如果不写v-if会发现，打开页面的时候显示的是最后一张图片-->
        <!--因为swiperList一开始传进来是空数组，接收ajax请求之后，再次重新渲染页面-->
        <!--此处的v-if,如果传递进来是空数组，v-if 里面是 false swiper就不会被创建-->
        <swiper :options="swiperOption" v-if="showSwiper">
            <!-- slides -->
            <swiper-slide v-for="item of list" :key="item.id">
                <img class="swiper-img" :src="item.imgUrl" alt="">
            </swiper-slide>
            <!-- Optional controls -->
            <!--slot 向父组件传递可以被自己定制的内容-->
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
        autoplay: true,
        speed: 2000
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
    .wrapper >>> .swiper-pagination-bullet-active
        background-color: #fff
    .wrapper
        overflow:hidden
        width:100%
        height:0
        padding-bottom:31.25%
        background-color: #eee
        .swiper-img
            width:100%
</style>
