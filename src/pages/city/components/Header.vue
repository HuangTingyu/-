<template>
    <div class="header">
        <router-link to="/">
            <span class="iconfont header-back">&#xe624;</span>
        </router-link>
        <span class="header-desc">城市选择</span>
    </div>
</template>

<script>
export default {
  name: 'CityHeader'
}
</script>

<style lang="stylus" scoped>
@import '~styles/varibles.styl'
.header
    position: relative;
    overflow:hidden;
    background-color: $bgColor;
    text-align: center;
    height:$headerHeight;
    line-height:$headerHeight;
    .header-desc
        position:absolute;
        left:50%;
        margin-left:-1rem;
        width:2rem;
        color:#fff;
        font-size:.32rem;
    .header-back
        position:absolute;
        top:0;
        left:0;
        width:.64rem;
        font-size:.4rem;
        text-align: center
        color:#fff;
</style>
