# Headline

> An awesome project.

## 灵感来自

[disoul/electron-cloud-music](https://github.com/disoul/electron-cloud-music)

[darknessomi/musicbox](https://github.com/darknessomi/musicbox)

[sqaiyan/netmusic-node](https://github.com/sqaiyan/netmusic-node)

## 10个Vue开发技巧

#### 1. 路由参数解耦

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