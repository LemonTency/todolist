# first-project

> my first vue-project

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```
## 本项目就是做一个todo  list ，用了vue
1. 用vue-cli直接一个项目 
2. 在app.vue里面直接修改 
3. 数值要在vue对象的data定义 
4. 方法要在Vue对象的method定义
5. for循环遍历
6. {{}} == v-text,是文本而不是 html
7. 记得加逗号

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).


#### 在文本框输入了一个newTodo之后，也需要在data数组里面进行类似声明的东西，不然会报错
Property or method "newTodo" is not defined on the instance but referenced during render. Make sure that this property is reactive, either in the data option, or for class-based components, by initializing the propert

//其意思主要就是说没有在对象中实例化


#### 是methods!!!!后面有s的

#### store.js里面两个函数我虽然也并不知道是什么意思，是直接复制过来的
#### 在store.js差点踩坑

1. window拼成windows  ，结果他说window也没有定义
2. 将.看成了逗号，结果他说stringify没有定义
3. console台还是能看出很多东西的

store.js完整代码如下：

        const STORAGE_KEY = "todos-vuejs"
        export default{
        fetch(){
            return JSON.parse(window.localStorage.getItem(STORAGE_KEY)||'[]')
         },
        save(todos){
            window.localStorage.setItem(STORAGE_KEY,JSON.stringify(todos))
        }
    }   // 这里面定义了两个方法,分别是fetch()和save()
    
************************* 
>localstorage是存储在浏览器本地的(了解了解setItem和getItem方法)

#### 添加watch的作用：在val有变化的时候，调用某个函数
深度watch函数写法如下：

    watch:{//观看状态的变化
        todos:{
        handler:function(todos){
        // console.log(val,oldVal)
            Store.save(todos);
        },
         deep:true//有这个todos的状态被改才有用
        }
    },

