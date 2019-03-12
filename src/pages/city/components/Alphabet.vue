<template>
    <ul class="list">
        <li class="item" v-for="item of letters" :key="item" @click="handleLetterClick"
            @touchstart="handleTouchStart" @touchmove="handleTouchMove" @touchend="handleTouchEnd" :ref="item">{{item}}</li>
    </ul>
</template>

<script>
export default {
  name: 'CityAlphabet',
  props: {
    cities: Object
  },
  computed: {
    letters () {
      const letters = []
      for (let i in this.cities) {
        letters.push(i)
      }
      return letters
    }
  },
  data () {
    return {
      touchStatus: false,
      startY: 0,
      timer: null
    }
  },
  updated () {
    this.startY = this.$refs['A'][0].offsetTop
  },
  methods: {
    handleLetterClick (e) {
      // 此处发射的是一个字母
      this.$emit('change', e.target.innerText)
    },
    handleTouchStart () {
      this.touchStatus = true
    },
    // 解释一下这里的定时器，按照这个设计，这个函数只能16ms被执行一次
    // 如果你超过这频率，比如16ms内执行了两次,
    // 你执行第2次的时候，它就会清掉你上一次的定时器
    // 结论就是，16ms内就算多次操作，这个函数也只会被执行一次
    handleTouchMove (e) {
      if (this.touchStatus) {
        if (this.timer) {
          clearTimeout(this.timer)
        }
        this.timer = setTimeout(() => {
          // offsetTop:当前元素顶部距离最近父元素顶部的距离,和有没有滚动条没有关系
          // 79是绿色方块的高度
          const touchY = e.touches[0].clientY - 79
          const index = Math.floor((touchY - this.startY) / 20)
          // 计算手指位置距A的距离，向下取整
          // 即粗略计算与A隔了几块字母，返回一个整数
          if (index >= 0 && index < this.letters.length) {
            // 根据返回的整数，发射一个字母给父组件
            this.$emit('change', this.letters[index])
          }
        }, 16)
      }
    },
    handleTouchEnd () {
      this.touchStatus = false
    }
  }
}
</script>

<style lang="stylus" scoped>
@import '~styles/varibles.styl'
.list
    display:flex;
    flex-direction:column;
    justify-content :center;
    position:absolute;
    top:1.58rem;
    right:0;
    bottom:0;
    width:.5rem;
    background: #ccc;
    .item
        color:$bgColor;
        font-size:.32rem;
        line-height: .4rem;
        text-align: center;
</style>
