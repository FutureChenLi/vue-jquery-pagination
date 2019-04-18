# vue-jquery-pagination
```
将jquery.pagination.js分页插件改为vue组件
```

## 安装yarn
```
npm install -g yarn
```
## Project setup
```
yarn install
```

### Compiles and hot-reloads for development
```
yarn run serve
```

### Compiles and minifies for production
```
yarn run build
```

### Run your tests
```
yarn run test
```

### Lints and fixes files
```
yarn run lint

vue-cli3 选择自定义 可以设置eslin，默认也有eslin，需要自定义设置
参照：https://www.jianshu.com/p/5e13bc2eb97c
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).

### 组件问题
```
1.父组件向子组件传参使用props即可传参
    a.方式
      props: {
          msg: String
        }
    b.方式
      props: [
          'msg'
        ]  
2.父组件动态改变子组件的内容，可将更改父组件的标签值，即传值时使用父组件的data即可
    并通过：v-bind:msg赋值
3.子组件向父组件传参
    子组件调用父组件，在父组件方法中修改父组件的参数
4.父组件调用子组件方法
    子组件方法：parentHandleclick
    父组件写法：
        先给使用组件的标签上ref标识
        通过使用this.$refs.标识.方法名
     如：
         <Page @changeP="changeMsg" ref="myChild" v-bind:msg="myMsg"/>
         this.$refs.myChild.parentHandleclick("我是爸爸");
5.子组件调用父组件方法
    使用this.$emit与自定义事件配合完成，如：
        子组件Page调用：
            this.$emit('changeP');
        父组件：
            <Page @changeP="changeMsg" v-bind:msg="myMsg"/>
        即可调用父组件的方法changeMsg
        
6.子组件与父组件交互对于input有个简写的方法，可以参照官方：在组件上使用 v-model

```

### vue
```vue
1. template 标签占位，可以用于for循环
2.方法在html中调用需要加()
3.template不会解析，所以v-show也是无用的

```


### ES6写法
```
1.{...s,...t}合并数据，已最后一个为准
```
