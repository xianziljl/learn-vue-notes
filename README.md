# VUE 学习笔记
a vue study notes.
## 参数与事件传递
有时候你想要传递所有参数 `(props)` 与事件 `(listeners)` 到子元件，但又不想要声明所有子元件的参数。你可以直接将 `$attrs` 与 `$listeners` 绑定在子元件上，并设定 `inheritAttrs` 为 `fals`e （若不设定后者，`div` 元素也会收到这些属性）。

```vue
<!-- 子组件 -->
<template>
  <div>
    <h1>{{title}}</h1>
    <child-component v-bind="$attrs" v-on="$listeners"></child-component>
  </div>
</template>

<script>
export default {
  name: 'PassingPropsSample'
  inheritAttrs: false,
  props: {
    title: {
      type: String,
      default: 'Hello, Vue!'
    }
  }
};
</script>
```
## 组件根元素为多个
当有时想在某个组件的根元素使用 `v-for` 的情况下是无法实现的，必须包裹再单独的根元素上，但可以使用 **渲染函数** 来实现这个需求。
```javascript
functional: true,
render (h, { props }) {
  return props.somePropItem.map(item =>
    <li key={item.id}>{item.name}</li>
  )
}
```
## watch 属性
`watch` 可以是一个字符串
```javascript
watch: {
  searchText: 'fetchUserList' // fetchUserList is a method.
}
```
`watch` 也可以是一个对象, `immediate: true` 表示在组件就绪后立即调用 `handler`.
```javascript
watch: {
  searchText: {
    handler: 'fetchUserList', // fetchUserList is a method.
    immediate: true
  }
}
```
## 组件根据路由参数刷新
```javascript
created () {
  this.getList(this.$route.params.id)
}
```
```html
<router-view :key="$route.fullPath"/>
```
