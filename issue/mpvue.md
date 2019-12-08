# mpVue

### 1. 在 swiper-items 使用 vuex 数据时页面卡顿

#### 项目描述

使用`vuex-persistedstate`负责持久化`vuex`的数据

#### 猜想原因

> 首次加载小程序时，`storage`内部不存在任何数据。此时`vuex-persistedstate`读取任意 key 的值为`undefined`，因此`vuex`内部变量的值亦为`undefined`，直接使用引起 bug 导致卡顿。

#### 解决方法

判断后再使用

```Javascript
computed: {
  ...mapGetters({
    productData: 'products'
  }),
  products () {
    return this.productData || []
  }
}
```
