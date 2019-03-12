<template>
    <!--template下面，一定要一个div包裹全部-->
    <!--不然会报错：-->
    <!--the template root requires exactly one element-->
    <div>
        <div class="title">周末去哪儿</div>
        <ul>
            <li class="item border-bottom" v-for="item of list" :key="item.id">
                <div class="item-img-wrapper">
                    <img class="item-img" :src="item.imgUrl">
                </div>
                <div class="item-info">
                    <p class="item-title">{{item.title}}</p>
                    <p class="item-desc">{{item.desc}}</p>
                </div>
            </li>
        </ul>
        <a href="#" class="see-all">查看所有产品</a>
    </div>
</template>

<script>
export default {
  name: 'HomeWeekend',
  props: {
    list: Array
  }
}
</script>

<style lang="stylus" scoped>
    @import '~styles/mixins.styl'
    .title
        line-height:.8rem
        background-color: #eee
        text-indent:.2rem
    .item-img-wrapper
        overflow: hidden
        height: 0
        /* 214/640 = 33.4% */
        padding-bottom: 37.4375%
        .item-img
            width:100%
    .item-info
        /*min-width:0 保证内容不超出外层容器*/
        padding:.14rem .2rem .2rem .2rem
        .item-title
            font-size:.28rem
            line-height:.48rem
            color:#222
            ellipsis ()
        .item-desc
            line-height: .4rem
            color:#666
            ellipsis ()
    .see-all
        display:block
        height:1rem
        line-height: 1rem
        text-align: center
        font-size: .32rem
        color:#00afc7
</style>
