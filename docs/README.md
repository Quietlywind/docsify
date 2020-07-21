# Headline

> An awesome project.

## 灵感来自

[disoul/electron-cloud-music](https://github.com/disoul/electron-cloud-music)

[darknessomi/musicbox](https://github.com/darknessomi/musicbox)

[sqaiyan/netmusic-node](https://github.com/sqaiyan/netmusic-node)

## 10个Vue开发技巧

### 1. 路由参数解耦

一般在组件内使用路由参数，大多数人会这样做：

```javascript
export default {
    methods: {
        getParamsId() {
            return this.$route.params.id
        }
    }
}
```

在组件中使用 `$route` 会使之与其对应路由形成高度耦合，从而使组件只能在某些特定的 URL 上使用，限制了其灵活性。

正确的做法是通过 `props` 解耦

```javascript
const router = new VueRouter({
    routes: [{
        path: '/user/:id',
        component: User,
        props: true
    }]
})
```

将路由的 `props` 属性设置为 `true` 后，组件内可通过 `props` 接收到 `params` 参数

```javascript
export default {
    props: ['id'],
    methods: {
        getParamsId() {
            return this.id
        }
    }
}
```

另外你还可以通过函数模式来返回 `props`

```javascript
const router = new VueRouter({
    routes: [{
        path: '/user/:id',
        component: User,
        props: (route) => ({
            id: route.query.id
        })
    }]
})
```

文档：[router.vuejs.org/zh](router.vuejs.org/zh)