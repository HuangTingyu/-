# -
Vue框架高仿去哪儿APP
## Vue框架高仿去哪儿

## 项目初始化

### CSS部分

- Main.js部分引入reset.css，初始化样式

- Border.css，防止1px边框在多倍屏手机上被显示称为多像素，原理scale方法

- Npm下载并引入fastClick插件，解决click事件的300ms延迟点击

### 插件部分

- Npm下载并引入fastClick插件，解决click事件的300ms延迟点击

- 使用fastClick，Main.js 输入 

  ```
  fastClick.attach(document.body)
  ```

  ​
