# vueshop

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

## Element-ui

### Asied

* element-ui 提供的组件,每个组件名都是它自己的类名

* 布局容器: Container Asied Main
  * 右侧菜单(二级可折叠) `el-menu`(最外层包裹菜单) `<el-submenu>`一级菜单 `<el-menu-item>` 二级菜单(里层)  `<template>` 菜单的模板(icon/span)

* 请求拦截器:  登录授权 请求验证是否有 token  需要授权的 API ，必须在请求头中使用 `Authorization` 字段提供 `token` 令牌
  * login 不需要 token 可以直接登录 登录进去后每次操作/请求都会验证 `Authorization` 的 token令牌

* 创建完成后立即发送 网络请求 请求左侧菜单栏的数据 get
  * 通过 async 和 await 来获取需要的数据 因为是数组所以可以使用 v-for 来遍历生成数据 第一级的icon不同的解决方法之一:定义一个对象来存放字体图标需要的类名  
  * 菜单栏只打开一个的可以给`el-menu` 添加 `unique-opened` 属性(1) 为 `true` |  折叠属性(2): `collapse` | 关闭过渡动画属性(3): `:collapse-transition="false"` | 
  * 左侧边栏的宽度变化(Aised): `:width="isCollapse ? '61px' : '200px'"` 利用三元表达式
  * 子菜单的跳转: `el-from` 有router(index属性)默认为false关闭的  index='/login' index做路由跳转
    * 里面的组件都是作为Home的子组件展示的,如果作为一个独立的路由而不是Home的子路由那么左侧的导航栏就销毁没有了
  * 左侧导航激活的高亮`:default-active="activePath"`: 点击导航-> 使用sessionStorage来保存激活的路径 并赋值给高亮的变量->  当离开再回来created时得到 sessionStorage 的路径 赋值给 高亮变量  (导航守卫.beforeEach)



* pm2 关闭命令行窗口依旧执行
  * npm i pm2 -g
    * 启动项目: pm2 start script --name(自定义名字)
    * 查看运行项目：pm2 ls 
    * 重启项目：pm2 restart 自定义名称
    * 停止项目：pm2 stop 自定义名称
    * 删除项目：pm2 delete 自定义名称
