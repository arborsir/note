# 一、ES6

## 声明变量

### var和let

- var 声明的变量往往会越域
- let 声明的变量有严格的局部作用域



执行下面代码，第二行输出则会报错：

```js
{
    var a = 1;
    let b = 2;
}

console.log(a);
console.log(b);
```



![image-20220405165115901](\..\.assets\4es和vue\image-20220405165115901.png)





- var 可以声明多次
- let 只能声明一次



```js
var a = 1;
var a = 3;
let b = 2;
let b = 4;
console.log(a);
console.log(b);
```



第二次声明b时报错：

![image-20220405165414143](\..\.assets\4es和vue\image-20220405165414143.png)



- var 会变量提升
- let 不存在变量提升

```js
console.log(a);
var a = 1;
console.log(b);
let b = 2;
```

到b的时候就报错了

![image-20220405165649213](\..\.assets\4es和vue\image-20220405165649213.png)

### const

常量，一旦声明，不允许改变

```js
const a = 1;
a = 3;
console.log(a);
```



![image-20220405165810274](\..\.assets\4es和vue\image-20220405165810274.png)	

## 解构表达式

### 数组解构

以前些写法是这样的：

```js
let arr = [1, 2, 3];
let a = arr[0];
let b = arr[1];
let c = arr[2];
console.log(a, b, c);
```



使用解构可以这样写，效果是一样的：

```js
let arr = [1, 2, 3];
        
let [a, b, c] = arr;
console.log(a, b, c);
```



### 对象解构

以前的写法：

```js
const person = {
    name: 'jack',
    age: 21,
    language: ['java', 'js', 'css']
} 
const name = person.name;
const age = person.age;
const language = person.language;
console.log(name, age, language);
```



解构写法：

```js
const person = {
    name: 'jack',
    age: 21,
    language: ['java', 'js', 'css']
} 
const {name, age, language} = person;
console.log(name, age, language);
```



也可以在解构的时候指定变量的名字：

```js
const person = {
    name: 'jack',
    age: 21,
    language: ['java', 'js', 'css']
} 
const {name:abc, age, language} = person;
console.log(abc, age, language);
```



## 字符串

### 字符串新的API

```js
let str = 'hello.vue';
console.log(str.startsWith('hello'));   // 是否以指定字符串开头
console.log(str.endsWith('.vue'));  // 是否以指定字符串结尾
console.log(str.includes('o')); // 是否包含子串
```



### 字符串模板

以前需要拼接字符串，现在使用反引号`搞定：

```js
        let ss = `<div>
    <span> hello world </span>
</div>`;

        console.log(ss);
```



输出结果：

![image-20220405171334541](\..\.assets\4es和vue\image-20220405171334541.png)

### 字符串插入变量和表达式

可以使用`${}`，在里面写变量、表达式、调用方法。

```js
function fun() {
    return '我不做舔狗了'
}
let name = '大冤种';
let age = 18;
let ss = `我是${name}，今年${age + 10}岁了，我想说：${fun()}。`;
console.log(ss);
```



![image-20220405171822507](\..\.assets\4es和vue\image-20220405171822507.png)



## 函数

### 函数参数默认值

以前的写法：

需要在方法里面判断是否为空，并设置默认值

```js
function add(a, b) {
    // 判断b是否为空，空的话给默认值 1 
    b = b || 1;
    return a + b;
}
console.log(add(10));
```



现在可以直接在方法声明处设置默认值，如果没传的话使用默认值：

```js
function add2(a, b = 1) {
    return a + b;
}
console.log(add2(20));
```



### 可变参数

```js
function fun(...values) {
    console.log(values.length);
}
fun(1, 2);
fun(3, 5, 7, 9, 11);
```



### 箭头函数

#### 单参数

以前的写法：

```js
var print = function(obj) {
    console.log(obj);
}
print("hello");
```



现在的写法：

```js
var print = obj => console.log(obj);
print("hello");
```



#### 多参数

以前的写法：

```js
var sum = function (a, b) {
    return a + b;
}
console.log(sum(1, 5));
```



现在的写法：

```js
var sum = (a, b) => a + b;
console.log(sum(1, 6));
```



#### 方法体多行代码

以前的写法：

```js
var sum = function (a, b) {
    a = a * 2 + b;
    return a + b;
};
console.log(sum(1, 6));
```

现在的写法：

```js
var sum = (a, b) => {
    a = a * 2 + b;
    return a + b;
};
console.log(sum(1, 6));
```



### 箭头函数+解构表达式

可以直接把传入的对象的name解构，并直接使用

```js
const person = {
    name: 'jack',
    age: 21,
    language: ['java', 'js', 'css']
}
var hello = ({name}) => console.log(name);
        
hello(person);
```



## 对象

### 新方法

三个方法：

```js
const person = {
    name: 'jack',
    age: 21,
    language: ['java', 'js', 'css']
}
console.log(Object.keys(person));   // 获取对象中所有的key
console.log(Object.values(person));   // 获取对象中所有的value
console.log(Object.entries(person));   // 将对象的元素转换为数组，数组的第一个值是key，第二个值是value
```



将对象合并：

```js
const target = {a: 1};
const source1 = {b: 2};
const source2 = {c: 3};
Object.assign(target, source1, source2);
console.log(target);
```

![image-20220405180845752](\..\.assets\4es和vue\image-20220405180845752.png)

### 声明对象新写法

以前的写法：

```js
const name = '张三';
const age = 21;
const person = {name: name, age: age}
console.log(person);
```



当对象中的key和value的属性名一样的时候，现在的写法：

```js
const name = '张三';
const age = 21;
const person = {name, age}
console.log(person);
```



### 对象的函数简写

```js
let person = {
    name: "李四",
    // 以前的写法
    eat: function(food) {
        // 获取对象中的属性需要使用this
        console.log(this.name + "在吃" + food);
    },
    // 箭头函数，箭头函数不能使用this，需要使用对象名来获取
    eat2: food => console.log(person.name + "在吃" + food),
    // 简写方式
    eat3(food) {
        console.log(this.name + "在吃" + food);
    }
}
person.eat("香蕉");
person.eat2("苹果");
person.eat3("梨");
```



![image-20220405181912560](\..\.assets\4es和vue\image-20220405181912560.png)

### 对象扩展运算符

这个运算符就是`...`

#### 拷贝对象(深拷贝)

```js
let person = {
    name: "李四",
    age: 15
}
let someone = {...person};
console.log(someone);
```



#### 合并对象

后赋的值，会覆盖初始值

```js
const name = {name: "王五"};
const age = {age: 34};
let person = {
    name: "李四",
    age: 15
}
person = {...name, ...age};
console.log(person);
```

![image-20220405182627698](\..\.assets\4es和vue\image-20220405182627698.png)

## 数组

### map方法

接收一个函数，将原数组中所有的元素用这个函数处理后放入新数组返回

```js
let arr = ['1', '20', '-1', '3'];
arr = arr.map((item) => {
    return item * 2
});
console.log(arr);
```

将字符串数组的每个元素 * 2 并返回一个新数组



简写：

```js
let arr = ['1', '20', '-1', '3'];
arr = arr.map(item => item * 2);
console.log(arr);
```



### reduce方法

`arr.reduce(callback, [initiaValue]);`

为数组的每个元素依次执行回调函数，不包括数组中被删除或从未被赋值的元素。

> 回调函数的四个参数：
>
> - `previousValue`：上一次调用回调返回的值，或是提供的初始值[initiaValue]
> - `currentValue`：数组中当前被处理的元素
> - `index`：当前元素在数组中的索引
> - `array`：调用reduce方法的数组



```js
let arr = [1, 20, -1, 3];
let arr2 = arr.reduce((a, b) => {
    console.log("上一次处理后的值：" + a);
    console.log("当前正在处理的元素：" + b);
    return a + b;
});
console.log(arr2);
```

可以得到结果：

![image-20220405194053124](\..\.assets\4es和vue\image-20220405194053124.png)



提供初始值：

```js
let arr = [1, 20, -1, 3];
let arr2 = arr.reduce((a, b) => {
    console.log("上一次处理后的值：" + a);
    console.log("当前正在处理的元素：" + b);
    return a + b;
}, 100);
console.log(arr2);
```

![image-20220405194331069](\..\.assets\4es和vue\image-20220405194331069.png)



## promise异步编排

### 准备

1. 先引入jQuery的依赖

   ```html
   <script src="https://cdn.bootcss.com/jquery/3.4.1/jquery.min.js"></script>
   ```

2. 编写三个json文件，模仿调用后端得到的返回信息

   user.json

   ```json
   {
       "id": 1,
       "username": "zhangsan",
       "password": "123456"
   }
   ```

   corse_1.json

   ```json
   {
       "id": 10,
       "name": "chinese"
   }
   ```

   score_10.json

   ```json
   {
       "id": 100,
       "score": 90
   }
   ```

3. 调用顺序就是：

   > 1. 查出当前用户信息
   > 2. 根据用户id查询课程信息
   > 3. 根据课程id查出分数信息

4. 编写ajax请求

   ```js
   $.ajax({
       url: "/json/user.json",
       success(data) {
           console.log("查询用户：", data);
           $.ajax({
               url: `json/corse_${data.id}.json`,
               success(data) {
                   console.log("查询到课程：", data);
                   $.ajax({
                       url: `json/score_${data.id}.json`,
                       success(data) {
                           console.log("查询到分数：", data);
                       }, 
                       error(error) {
                           console.log("出现了错误：", error);
                       }
                   });
               },
               error(error) {
                   console.log("出现了错误：", error);
               }
           });
       },
       error(error) {
           console.log("出现了错误：", error);
       }
   });
   ```

5. 可以看到控制台的输出

   ![image-20220405200939680](\..\.assets\4es和vue\image-20220405200939680.png)



### 使用promise

Promise可以封装异步操作，把**无线嵌套**变成了**链条**。

```js
let p = new Promise((resolve, reject) => {
    // resolve是成功后要做的事情，reject是失败后要做的事情
    // 使用ajax发送请求
    $.ajax({
        url: "/json/user.json",
        success(data) {
            console.log("查询用户：", data);
            resolve(data);  // 把数据传进去，好操作
        },
        error(error) {
            console.log("出现了错误：", error);
            reject(error);
        }
    });
});
// then 成功后的操作
p.then((obj) => {
    // 发送第二次请求，并将结果封装为Promise
    return new Promise((resolve, reject) => {
        $.ajax({
            url: `json/corse_${obj.id}.json`,
            success(data) {
                console.log("查询到课程：", data);
                resolve(data);
            },
            error(error) {
                console.log("出现了错误：", error);
                reject(error);
            }
        });
    })
}).then((obj) => {
    // 发送第三次请求，因为没有new Promise所以没有resolve和reject方法
    $.ajax({
        url: `json/score_${obj.id}.json`,
        success(data) {
            console.log("查询到分数：", data);
        },
        error(error) {
            console.log("出现了错误：", error);
        }
    });
})
```



可以封装发送请求的方法，更简单，更简便：

```js
function get(url, data) {
    return new Promise((resolve, reject) => {
        $.ajax({
            url: url,
            data: data,
            success(data) {
                resolve(data);
            },
            error(error) {
                reject(error);
            }
        });
    })
}
get("json/user.json")
    .then((data) => {
        console.log("查询用户：", data);
        return get(`json/corse_${data.id}.json`);
    })
    .then(data => {
        console.log("查询到课程：", data);
        return get(`json/score_${data.id}.json`);
    })
    .then(data => {
        console.log("查询到分数：", data);
    })
    .catch(err => {
        console.log("出现了错误：", error);
    });
```



## 模块化

### export导出

export不仅可以导出对象，也可以导出JS的一切变量，比如基本类型变量、函数、数组、对象。

```js
var name = "zhangsan";
var age = 32;

function add(a, b) {
    return a + b;
}

export { name, age, add }
```



```js
const util = {
    sum(a, b) {
        return a + b;
    }
}
export { util }
```



也可以在声明的时候导出：

```js
export const util = {
    sum(a, b) {
        return a + b;
    }
}
```



也可以在导出的时候不指定名字，这样导入的时候就可以随便起名：

```js
export default {
    sum(a, b) {
        return a + b;
    }
}

import abc from "./hello";
abc.sum(1, 2);
```





### import导入

可以只导入需要的东西

```js
import { name, add } from "./user";
import util from "./hello";

util.sum(1, 2);
console.log(name);
add(3, 4);
```



# 二、VUE

## 安装

使用npm初始化项目

```bash
npm init -y
```

package.json文件表示，这个是使用npm管理的项目

![image-20220406204104094](\..\.assets\4es和vue\image-20220406204104094.png)



安装vue：

现在使用该命令默认安装的是vue3

```bash
npm install vue
```

安装vue2的话需要使用：

```bash
npm i vue@2
```





## 基本语法

### 声明式渲染

创建一个`index.html`文件，动态绑定，可以把对象中的值，实时输出到页面上

```html
<div id="app">
    <h1>{{name}}，非常帅</h1>
</div>
<script src="./node_modules/vue/dist/vue.js"></script>
<script>
    let vm = new Vue({
        el: "#app",
        data: {
            name: "张三"
        }
    });
</script>
```



### v-model 双向绑定

模型变化，视图变化。视图变化，模型变化。

```html
<div id="app">
    <input type="text" v-model="num">
    <h1>{{name}}，非常帅，有{{num}}个人给他点赞</h1>
</div>
<script src="./node_modules/vue/dist/vue.js"></script>
<script>
    let vm = new Vue({
        el: "#app",
        data: {
            name: "张三",
            num: 1
        }
    });
</script>
```

可以实时的将输入框中的值，放到h1标签中

![image-20220406205705809](\..\.assets\4es和vue\image-20220406205705809.png)



也可以直接在控制台修改变量的值：

![image-20220406205952096](\..\.assets\4es和vue\image-20220406205952096.png)

### v-on 事件绑定

```html
<div id="app">
    <input type="text" v-model="num">
    <button v-on:click="num++">点赞</button>
    <h1>{{name}}，非常帅，有{{num}}个人给他点赞</h1>
</div>
<script src="./node_modules/vue/dist/vue.js"></script>
<script>
    let vm = new Vue({
        el: "#app",
        data: {
            name: "张三",
            num: 1
        }
    });
</script>
```



点赞按钮实现每点击一下，num进行++操作



**绑定方法：**

```html
<div id="app">
    <input type="text" v-model="num">
    <button v-on:click="num++">点赞</button>
    <button v-on:click="cancel">取消点赞</button>
    <h1>{{name}}，非常帅，有{{num}}个人给他点赞</h1>
</div>
<script src="./node_modules/vue/dist/vue.js"></script>
<script>
    let vm = new Vue({
        el: "#app",
        data: {
            name: "张三",
            num: 1
        },
        methods:{
            // 所有的方法放这里
            cancel(){
                this.num--;
            }
        }
    });
</script>
```



### 总结

1. 创建vue实例，关联页面模板，可以将自己的数据(data)渲染到关联的模板，响应式的
2. 使用指令来简化对dom的一些操作
3. 声明方法来做更复杂的操作，methods中可以封装方法。
4. `new Vue`中的：
   - el：绑定元素
   - data：封装数据
   - methods：封装方法



## 安装插件

语法提示插件

![image-20220406211048531](\..\.assets\4es和vue\image-20220406211048531.png)



浏览器的插件

[Home | Vue Devtools (vuejs.org)](https://devtools.vuejs.org/)

谷歌商店：[Vue.js devtools - Chrome 网上应用店 (google.com)](https://chrome.google.com/webstore/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd/related?utm_source=www.crx4chrome.com)

方便调试



## Vue指令

### v-html 转义HTML标签

### v-text 显示原字符

```html
<div id="app">
    {{msg}}
    <br>
    <span v-html="msg"></span>
    <span v-text="msg"></span>
</div>
<script>
    new Vue({
        el: "#app",
        data: {
            msg: "<h1>hello</h1>"
        }
    });
</script>
```





![image-20220406220248903](\..\.assets\4es和vue\image-20220406220248903.png)

### 插值表达式

格式：`{{表达式}}`，只能写在标签体里面

- 该表达支持js语法，可以调用js内置函数(必须有返回值)
- 表达式必须有返回结果，例如`1 + 1`，没有结果的表达式不允许，例如`let a = 1 + 1`
- 可以直接获取Vue实例中定义的数据或函数

```html
<div id="app">
    {{msg}}{{hello()}}{{1 + 1}}
</div>
<script>
    new Vue({
        el: "#app",
        data: {
            msg: "<h1>hello</h1>"
        },
        methods: {
            hello(){
                return "world";
            }
        },
    });
</script>
```



#### 插值闪烁

使用{{}}在网速比较慢时会出现，在页面未加载完之前，页面会显示原始的`{{}}`，加载完毕后才显示正确的数据。



### v-bind 给标签属性绑定值

在需要绑定vue中值的html属性前加上`v-bind:`即可，也可以缩写，直接写一个冒号就行`:`

```html
<div id="app">
    <a v-bind:href="link">gogogo</a>
</div>
<script>
    new Vue({
        el: "#app",
        data: {
            link: "https://www.baidu.com"
        }
    });
</script>
```



v-bind指令对class属性和style属性有增强

当isActive的值为true的时候，span标签中的class属性才有active，当hasError为ture的时候，class属性才有text-danger。

```html
<div id="app">
    <span v-bind:class="{active:isActive, 'text-danger':hasError}">你好</span>
</div>
<script>
    new Vue({
        el: "#app",
        data: {
            isActive: true,
            hasError: true
        }
    });
</script>
```



style同理：

可以在Vue对象中指定style的值，`'font-size'`可以写成`fontSize`

```html
<div id="app">
    <span v-bind:style="{color: color1,'font-size': size}">你好</span>
</div>
<script>
    new Vue({
        el: "#app",
        data: {
            color1: 'red',
            size: '90px'
        }
    });
</script>
```



### v-model 双向绑定

这里会将选择的存入language数组中，并且直接在页面上展现，也可以通过改变数组中的值，来修改页面上的是否选中

```html
<div id="app">
    精通的语言：<br>
    <input type="checkbox" v-model="language" value="Java">Java<br>
    <input type="checkbox" v-model="language" value="C++">C++<br>
    <input type="checkbox" v-model="language" value="PHP">PHP<br>
    选中了：<br>
    {{language.join(',')}}
</div>
<script>
    new Vue({
        el: "#app",
        data: {
            language: []
        }
    });
</script>
```

