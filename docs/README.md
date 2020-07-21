# Headline

> An awesome project.

<!-- ## 灵感来自

[disoul/electron-cloud-music](https://github.com/disoul/electron-cloud-music)

[darknessomi/musicbox](https://github.com/darknessomi/musicbox)

[sqaiyan/netmusic-node](https://github.com/sqaiyan/netmusic-node) -->

## Vue开发技巧

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

### 2. 函数式组件

函数式组件是无状态，它无法实例化，没有任何的生命周期和方法。创建函数式组件也很简单，只需要在模板添加 `functional` 声明即可。一般适合只依赖于外部数据的变化而变化的组件，因其轻量，渲染性能也会有所提高。

组件需要的一切都是通过 `context` 参数传递。它是一个上下文对象，具体属性查看文档。这里 `props` 是一个包含所有绑定属性的对象。

函数式组件

```javascript
<template functional>
    <div class="list">
        <div class="item" v-for="item in props.list" :key="item.id" @click="props.itemClick(item)">
            <p>{{item.title}}</p>
            <p>{{item.content}}</p>
        </div>
    </div>
</template>
```

父组件使用

```javascript
<template>
    <div>
        <List :list="list" :itemClick="item => (currentItem = item)" />
    </div>
</template>
```

```javascript
import List from '@/components/List.vue'
export default {
    components: {
        List
    },
    data() {
        return {
            list: [{
                title: 'title',
                content: 'content'
            }],
            currentItem: ''
        }
    }
}
```

文档：[cn.vuejs.org/v2/guide](cn.vuejs.org/v2/guide)
