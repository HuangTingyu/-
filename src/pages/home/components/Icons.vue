<template>
    <div class="icons">
        <swiper :options="swiperOption">
            <swiper-slide  v-for="(page,index) of pages" :key="index">
                <div class="icon" v-for="item of page" :key="item.id">
                    <div class="icon-img">
                        <img class='icon-img-content' :src="item.imgUrl">
                    </div>
                    <p class="icon-desc">{{item.desc}}</p>
                </div>
            </swiper-slide>
        </swiper>
    </div>
</template>

<script>
export default {
  name: 'HomeIcons',
  props: {
    list: Array
  },
  data () {
    return {
      swiperOption: {
        autoplay: false
      }
    }
  },
  computed: {
    pages () {
      // 根据上面item的数量，这个函数会返回1个包含两个元素的二维数组
      const pages = []
      // forEach() 方法用于调用数组的每个元素，并将元素传递给回调函数。
      this.list.forEach((item, index) => {
        // 这里floor进行向下取整，
        // 如果floor(index / 8)=0,item就会被存放在pages[0]里面
        // 如果floor(index / 8)=1,item就会被存放在pages[1]里面
        // ......以此类推
        // 如果pages[page]不存在,就令它等于一个空数组
        const page = Math.floor(index / 8)
        if (!pages[page]) {
          pages[page] = []
        }
        pages[page].push(item)
      })
      return pages
    }
  }
}
</script>

<style lang="stylus" scoped>
    @import '~styles/varibles.styl'
    @import '~styles/mixins.styl'
    .icons >>> .swiper-container
        height: 0
        padding-bottom: 50%
    .icon
        float:left
        overflow:hidden
        position:relative
        width:25%
        height:0
        padding-bottom:25%
        .icon-img
            position:absolute
            top: 0
            left:0
            right:0
            bottom:.44rem
            box-sizing:border-box
            padding:.1rem
            .icon-img-content
                display:block
                margin:0 auto
                height:100%
        .icon-desc
            text-align: center
            color:$darkTextColor
            position:absolute
            left:0
            right:0
            bottom:0rem
            height:.44rem
            line-height .44rem
            ellipsis ()
</style>
