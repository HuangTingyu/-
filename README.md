## Vue框架高仿去哪儿

## 项目启动方式

```
cd Travel
cnpm install
npm run dev
```

## 项目初始化

### 路径部分（webpack.base.conf.js）

找到resolve部分，这里可以配置从而实现简化路径的目的。

```
resolve: {
    extensions: ['.js', '.vue', '.json'],
    alias: {
      'vue$': 'vue/dist/vue.esm.js',
      '@': resolve('src'),
      'styles':resolve('src/assets/styles'),
      'common':resolve('src/common')
    }
  },
```

使用方法如下，这里的~styles就指代src/assets/styles

```
@import '~styles/varibles.styl'
```

### CSS部分

- Main.js部分引入reset.css，初始化样式,修改html的fontsize，因为设计稿是2倍图，宽度为86px的组件在fontsize修改之后，就成了.86rem

  ```
  font-size:50px
  ```

- Border.css，防止1px边框在多倍屏手机上被显示称为多像素，原理scale方法

- Npm下载并引入fastClick插件，解决click事件的300ms延迟点击

- 安装Stylus

  ```
  cnpm install stylus --save
  cnpm isntall stylus-loader --save
  ```

  引入stylus

  ```
  <style lang="stylus" scoped>
  ```

  stylus变量使用，在css目录下建立varibles.styl,保存背景颜色

  ```
  $bgColor = #00bcd4
  ```

  header.vue引用

  ```
  @import '~styles/varibles.styl'
  ```

  解决报错，修改完webpack配置项之后，一定要重启项目npm run dev

### 插件部分

- cnpm下载并引入fastClick插件，解决click事件的300ms延迟点击

- 使用fastClick，Main.js 输入 

  ```
  fastClick.attach(document.body)
  ```

### 字体文件

阿里巴巴字体图标库下载完成之后，assets/styles/iconfont存入iconfont.eot，iconfont.svg，iconfont.ttf以及iconfont.woff四个文件，iconfont.css放在styles目录下即可，把iconfont.css文件中的url部分修改为正确的存储路径。

记得main.js引入iconfont.css。

## 首页头部开发(header.vue)

```
<style lang="stylus" scoped>
```

