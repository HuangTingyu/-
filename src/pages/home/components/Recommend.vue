<template>
    <!--template下面，一定要一个div包裹全部-->
    <!--不然会报错：-->
    <!--the template root requires exactly one element-->
    <div>
    <div class="recommend-title">热销推荐</div>
    <ul>
        <router-link tag="li" :to="'/detail/'+item.id" class="item border-bottom" v-for="item of list" :key="item.id">
                <img class="item-img" :src="item.imgUrl">
            <div class="item-info">
                <p class="item-title">{{item.title}}</p>
                <p class="item-desc">{{item.desc}}</p>
                <button class="item-button">查看详情</button>
            </div>
        </router-link>
    </ul>
        <a href="#" class="see-all">查看所有产品</a>
    </div>
</template>

<script>
export default {
  name: 'HomeRecommend',
  props: {
    list: Array
  }
}
</script>

<style lang="stylus" scoped>
    @import '~styles/mixins.styl'
    .recommend-title
        margin-top:.2rem
        line-height:.8rem
        background-color: #ccc
        text-indent:.2rem
    .item
        display:flex
        height:1.9rem
        overflow:hidden
        .item-img
            width:1.7rem
            height:1.7rem
            padding:.1rem
        .item-info
            /*min-width:0 保证内容不超出外层容器*/
            padding:.1rem
            flex:1
            min-width:0
            .item-title
                font-size:.4rem
                line-height:.54rem
                ellipsis ()
            .item-desc
                line-height: .4rem
                color:#ccc
                ellipsis ()
        .item-button
            line-height: .44rem
            margin-top:.16rem
            margin-top: .2rem
            background-color: #ff9300;
            padding: 0 .2rem
            color:#fff
            border-radius:.06rem
    .see-all
        display:block
        height:1rem
        line-height: 1rem
        text-align: center
        font-size: .32rem
        color:#00afc7
</style>
