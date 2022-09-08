# `Vue`

## `Vue`基础

### `Vue`简介

`Vue`是一个`JavaScript`框架，它简化了`DOM`操作且是响应式数据驱动。

### 第一个`Vue`程序

开发第一个`Vue`程序的步骤：

1. 导入开发版本的`Vue.js`
2. 创建`Vue`实例对象，设置`el`属性和`data`属性
3. 使用简洁的模板语法`{{}}`将数据渲染到页面上

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vue基础</title>
</head>
<body>
    <div id="app">
        {{ message }}
    </div>
    <!--导入 Vue.js -->
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
    <script>
        var app = new Vue({
            el: "#app",
            data:{
                message: "Hello Vue!"
            }
        })
    </script>
</body>
</html>
```

### `el`：挂载点

1. 上面使用的是`id`是否可以使用其它的选择器？

   **都是可以的，但是因为`id`一般都是唯一的所以建议使用`id`选择器。**

2. `Vue`的作用域在哪里？

   **`Vue`会管理`el`选项命中的元素及其内部的后代元素**

3. 是否可以设置其它的`dom`元素呢？

   **可以使用其它的双标签但是不能使用`html body`标签**

4. `el`的作用？

   **设置`Vue`实例挂载点，说白了就是你要操作管理哪个`DOM`**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>el:挂载点</title>
</head>
<body>
    <div id="app" class="app">
        {{ message }}
        <span>{{ message }}</span>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
    <script>
        var app = new Vue({
            //el: "#app", id选择器
            //el: ".app", 类选择器
            el: "div",//标签选择器
            data: {
                message: "Hello Vue2!"
            }
        })
    </script>
</body>
</html>
```

### `data`：数据对象

- `Vue`中使用到的数据定义在`data`中
- `data`中可以写复杂类型的数据
- 渲染复杂类型的数据时，遵守`JavaScript`的语法即可

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>data：数据对象</title>
</head>
<body>
    <div id="app">
        {{ message }}
        <h2>{{ vongala.name }}</h2>
        <h3>{{ vongala.ring }}</h3>
        <ul>
            <li>{{ rings[0] }}</li>
            <li>{{ rings[1] }}</li>
            <li>{{ rings[2] }}</li>
            <li>{{ rings[3] }}</li>
            <li>{{ rings[4] }}</li>
            <li>{{ rings[5] }}</li>
            <li>{{ rings[6] }}</li>
        </ul>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
    <script>
        var app = new Vue({
            el: "#app",
            data: {
                message: "Hello Vue Data!",
                vongala: {
                    name: "彭哥列家族",
                    ring: "一共 7 枚戒指"
                },
                rings: ["空", "岚", "雨", "云", "雾", "晴", "雷"]
            }
        })
    </script>
</body>
</html>
```

## `Vue`本地应用

现在不用使用纯`JS`代码操作`DOM`了而是使用`Vue`指令。

### 内容绑定，事件绑定

#### `v-text`

作用：将数据设置给标签的文本值

- `v-text`指令的作用：设置标签的内容`textContent`
- 默认写法会替换全部内容，使用差值表达式`{{}}`可以替换指定内容适用于部分内容

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>v-text</title>
</head>
<body>
    <div id="app">
        <h2 v-text="message"></h2>
        <!--设置全部内容-->
        <h2 v-text="'彭哥列'+message"></h2>
        <!--设置部分内容-->
        <h2>西蒙{{ message }}</h2>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
    <script>
        var app = new Vue({
            el: "#app",
            data: {
                message: "家族"
            }
        })
    </script>
</body>
</html>
```

#### `v-html`

- 类似于`v-text`，设置的是`html`结构比如解析为的字段为`<a href="">111</a>`如果使用的是`v-text`会被设置成文本，但是使用`v-html`会被解析为`html`结构。

  如何选择？有`html`结构就选择`v-html`，如果没有就选择`v-text`即可。

- `v-html`指令的作用是：设置元素的`innerHTML`

- 内容中有`html`结构会被解析为标签

- `v-text`指令无论内容是什么，只会解析为文本

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>v-html</title>
  </head>
  <body>
      <div id="app">
          <p v-html="content"></p>
          <p v-text="content"></p>
      </div>
      <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
      <script>
          var app = new Vue({
              el: "#app",
              data: {
                  content: "<h1>彭哥列家族</h1>"
              }
          })
      </script>
  </body>
  </html>
  ```

#### `v-on`基础

- `v-on`指令的作用是：为元素绑定事件

- 事件名不需要写`on`可以直接简写为`@`

- 绑定的方法定义在`methods`属性中

- 方法内部通过`this`关键字可以访问定义在`data`中的数据

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>v-on</title>
  </head>
  <body>
      <div id="app">
          <input type="button" value="单击事件v-on:" v-on:click="mymethod"/>
          <input type="button" value="鼠标触发v-on:" v-on:mouseenter="mymethod"/>
          <input type="button" value="双击事件v-on:" v-on:dblclick="mymethod"/>
          <input type="button" value="双击事件@" @dblclick="mymethod"/>
          <h2 @click="changefood" v-text="food"></h2>
      </div>
      <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
      <script>
          var app = new Vue({
              el: "#app",
              data: {
                  food: "西红柿炒蛋"
              },
              methods: {
                  mymethod:function(){
                      alert("Vongala")
                  },
                  changefood:function(){
                      this.food += "好好吃！"
                  }
              }
          })
      </script>
  </body>
  </html>
  ```

#### `v-text v-html v-on`案例

模拟计数器：默认起始值为`1`，数据范围为：`0 - 10`

![img](https://img-blog.csdnimg.cn/567403ff1d2744d0887c0fc1d1601d65.png)

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Document</title>
    <style>
      #app {
        width: 480px;
        height: 100px;
        margin: 200px auto;
      }
      .input-num {
        margin-top: 20px;
        height: 100%;
        display: flex;
        border-radius: 10px;
        overflow: hidden;
        box-shadow: 0 0 4px black;
      }
      .input-num button {
        width: 150px;
        height: 100%;
        font-size: 40px;
        color: gray;
        cursor: pointer;
        border: none;
        outline: none;
      }
      .input-num span {
        height: 100%;
        font-size: 40px;
        flex: 1;
        text-align: center;
        line-height: 100px;
      }
    </style>
  </head>
  <body>
    <div id="app">
      <!-- 计数器 -->
      <div class="input-num">
        <button @click="add">+</button>
        <span v-text="num"></span>
        <button @click="sub">-</button>
      </div>
    </div>
  </body>
</html>
<!-- 开发环境版本，包含了有帮助的命令行警告 -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<!-- 编码 -->
<script>
    var app = new Vue({
        el: "#app",
        data: {
            num: 1
        },
        methods: {
            add:function(){
                if(this.num == 10) {
                    alert("别点啦，到头啦！");
                    return;
                };
                this.num += 1;
            },
            sub:function(){
                if(this.num == 0) {
                    alert("别点啦，到底啦！");
                    return;
                };
                this.num -= 1
            }
        }
    })
</script>
```

### 显示切换，属性绑定

#### `v-show`

- `v-show`指令作用：根据表达值得真假，切换元素的显示和隐藏

- 原理是修改元素的`display`，实现元素的显示/隐藏

- 指令后面的内容最终都会解析为布尔值

- 值为`true`显示元素，值为`false`隐藏元素

- `v-show`判断内容可以直接写表达式

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>Document</title>
  </head>
  <body>
      <div id="app">
          <button @click="subAge">点我减小年龄！</button>
          <button @click="addAge">点我增大年龄！</button>
          <h2 v-text="'当前年龄为：' + age + '岁！[18 岁以上包括 18 岁可以看照片哦~]'"></h2>
          <img src="https://th.bing.com/th/id/OIP.xynOAVXBTdCCBCBPOW42VwHaH4?w=142&h=180&c=7&r=0&o=5&dpr=1.5&pid=1.7" v-show="isShow"></img>
      </div>
      <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
      <script>
          var app = new Vue({
              el: "#app",
              data: {
                  isShow: false,
                  age: 1
              },
              methods:{
                  subAge:function(){
  
                      if(this.age <= 1) {
                          alert("已经是目前人类的最小年龄啦！！！");
                          return;
                      };
                      this.age -= 1;
                      if(this.age < 18) {
                          this.isShow = false;
                      };
                  },
                  addAge:function(){
                      if(this.age >= 140) {
                          alert("已经是目前人类的最大年龄啦！！！");
                          return;
                      };
                      this.age += 1;
                      if(this.age >= 18) {
                          this.isShow = true;
                      };
                  }
              }
          })
      </script>
  </body>
  </html>
  ```

#### `v-if`

- `v-if`指令的作用：跟`v-show`类似，都是根据表达式的真假切换元素的显示状态

- 本质就是通过`dom`元素来切换显示状态

- 表达式的值为`true`，元素存在于`dom`树种，为`false`元素从`dom`树种移除

- 频繁的切换使用`v-show`，反之使用`v-if`，操作`DOM`树是非常消耗性能的所以前者切换消耗性能小

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>v-if</title>
  </head>
  <body>
      <div id="app">
          <h2 v-if="1 == 1" v-text="message"></h2>
      </div>
      <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
      <script>
          var app = new Vue({
              el: "#app",
              data: {
                  isIf: true,
                  message: "Vongala"
              }
          })
      </script>
  </body>
  </html>
  ```

#### `v-bind`

- `v-bind`指令的作用是：设置元素的属性比如`src title class`，都是元素内部的属性

- 完整写法是：`v-bind:属性名`

- 简写的话可以直接省略`v-bind`，只保留：`:属性名`

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>v-bind</title>
      <style>
          .active{
              border: 1px solid red
          }
      </style>
  </head>
  <body>
      <div id="app">
          <img v-bind:src="imgSrc">
          <img v-bind:src="imgSrc" v-bind:title="imgTitle+'!!!!!!'" v-bind:class="isActive?'active':''" @click="toggleActive"></img>
          <img v-bind:src="imgSrc" v-bind:title="imgTitle+'!!!!!!'" v-bind:class="{active:isActive}" v-on:click="toggleActive"></img>
          <img :src="imgSrc" :title="imgTitle" :class="{active:isActive}"/>
      </div>
      <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
      <script>
          var app = new Vue({
              el: "#app",
              data: {
                  imgSrc: "https://www.imgacademy.com/sites/default/files/venue-golf-pg11.jpg",
                  imgTitle: "Vongala",
                  isActive: true
              },
              methods: {
                  toggleActive:function(){
                      this.isActive = !this.isActive;
                  }
              }
          })
      </script>
  </body>
  </html>
  ```

#### `v-show v-if v-bind`案例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="./css/index.css">
    <title>图片切换案例</title>
</head>
<body>
    <div id="mask">
        <div class="center">
            <h2 class="title">
              <img src="./images/logo.png" alt="">
                Vongala
            </h2>
            <a href="javascript:void(0)" v-show="imgSrcNum" class="left" @click="prev"><img src="./images/prev.png" alt=""></a>
            <img :src="'./images/'+indexImages[imgSrcNum]+'.jpg'"/>            
            <a href="javascript:void(0)" v-show="imgSrcNum<indexImages.length-1" @click="next" class="right"><img src="./images/next.png" alt=""></a>
        </div>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
    <script>
        var app = new Vue({
            el: "#mask",
            data: {
                indexImages: ["00","01","02","03","04","05","06","07","08","09","10"],
                index: 0,
                imgSrcNum: 0
            },
            methods: {
                prev:function(){
                    this.imgSrcNum--;
                },
                next:function(){
                    this.imgSrcNum++;
                }
            }
        })
    </script>
</body>
</html>
```

### 列表循环，表单元素绑定

#### `v-for`

- `v-for`指令的作用是：根据数据生成列表结构
- 数组经常和`v-for`结合使用，语法为：`(item, index) in 数据`
- `item`和`index`可以结合其他指令一起使用
- 数组长度的更新会同步到页面上，是响应式的

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>v-for</title>
</head>
<body>
    <div id="app">
        <ul>
            <li v-for="(people, index) in vongala">{{ people.rings }} - {{ people.name }}</li>
        </ul>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
    <script>
        var app = new Vue({
            el: "#app",
            data: {
                vongala: [
                    {
                        name: "沢田纲吉",
                        rings: "大空"
                    },
                    {
                        name: "狱寺隼人",
                        rings: "岚守"
                    },
                    {
                        name: "山本武",
                        rings: "雨守"
                    },
                    {
                        name: "云雀恭弥",
                        rings: "云守"
                    },
                    {
                        name: "蓝波",
                        rings: "雷守"
                    },
                    {
                        name: "六道骸",
                        rings: "雾守"
                    },
                    {
                        name: "笹川了平",
                        rings: "晴守"
                    },
                ]
            }
        })
    </script>
</body>
</html>
```

#### `v-on`补充

- `v-on`除了普通的绑定事件，还可以传递自定义参数也就是可以写成函数调用的形式

- 定义方法时需要定义形参来接收传入的实参

- 事件的后面跟上`.修饰符`可以对事件进行限制

- `.enter`可以限制触发的按键为回车

- 事件修饰符有多种

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>v-on</title>
  </head>
  <body>
      <div id="app">
          <input type="button" @click="myMethod('牛', '逼')" value="点我啊大笨蛋"/>
          <input type="text" @keyup.enter="sayHi"/>
      </div>
      <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
      <script>
          var app = new Vue({
              el: "#app",
              data: {
                  food: "西红柿炒蛋"
              },
              methods: {
                  myMethod:function(a, b){
                      alert(a + b);
                  },
                  sayHi:function(){
                      console.log("开饭啦！！！");
                  }
              }
          })
      </script>
  </body>
  </html>
  ```

#### `v-model`

- **`v-model`只能操作表单元素**

- `v-model`指令的作用是便捷的设置和获取表单元素的值

- 绑定的数据会和表单元素值相关联

- 绑定的数据 <---> 表单元素的值【双向绑定】

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>v-model</title>
  </head>
  <body>
      <div id="app">
          <input type="text" v-model="message"/>
          <h2 v-text="message"></h2>
      </div>
      <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
      <script>
          var app = new Vue({
              el: "#app",
              data: {
                  message: "彭哥列家族的首领草帽路飞打败了最终BOSS辉夜"
              }
          })
      </script>
  </body>
  </html>
  ```

#### `v-for v-on v-model`案例

记事本案例：新增、删除、统计、清空、隐藏

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>记事本案例</title>
    <link rel="stylesheet" href="./css/indexlog.css"/>
</head>
<body>
    <!--主体区域-->
    <section id="todoapp">
        <header class="header">
            <h1>MyTodoList</h1>
            <input type="text" v-model="inputValue" autocomplete="off" autofocus="autofocus" @keyup.enter="addPlan" placeholder="请输入任务" class="new-todo"/>
        </header>
        <!--列表区域-->
        <section class="main">
            <ul class="todo-list">
                <li v-for="(plan, index) in todoList">
                    <div class="view">
                        <span class="index">{{ index + 1 }}</span>
                        <label>{{ plan }}</label>
                        <button class="destroy" @click="removePlan(index)"></button>
                    </div>
                </li>
            </ul>
        </section>
        <!--统计和清空区域-->
        <footer class="footer">
            <span v-show="todoList.length!=0" class="todo-count" v-text="'共 ' + todoList.length + ' 个计划'"></span>
            <button v-show="todoList.length!=0" class="clear-completed" @click="clearList">清空</button>
        </footer>
    </section>
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
    <script>
        var app = new Vue({
            el: "#todoapp",
            data: {
                inputValue: "",
                todoList: ["吃饭", "睡觉", "打豆豆"]
            },
            methods: {
                addPlan:function(){
                    this.todoList.push(this.inputValue);
                    this.inputValue = "";
                },
                removePlan:function(index){
                    this.todoList.splice(index, 1);
                },
                clearList:function(){
                    this.todoList = [];
                }
            }
        })
    </script>
</body>
</html>
```

## `Vue`网络应用

### `axios`

- `axios`必须先导入才可以使用
- 使用`get`或`post`方法即可发送对应的请求
- `then`方法种的回调函数会在请求成功或者失败的时候触发
- 通过回调函数的形参可以获取响应内容，或者错误信息

```html
<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>axios基本使用</title>
</head>
<body>
    <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
    <script>
        axios.get("https://autumnfish.cn/api/joke/list?num=6").then(function(response){
            console.log(response.data.data);
        }, function(error){
            console.log(error);
        });
        axios.post("https://autumnfish.cn/api/user/reg", {
            "username":"彭哥列家族"
        }).then(function(response){
            console.log(response)
        }, function(error){
            console.log(error);
        });
    </script>
</body>
</html>
```

### `axios + vue`

- `vue`网络应用和本地应用的最大区别就是改变了数据来源
- `axios`回调函数中无法通过`this`直接获取到`Vue`，因为此时`this`根本不指向`vue`实例，正确的做法是：将`this`保存起来，然后在回调函数中直接使用保存的`this`即可

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>axios + vue</title>
</head>
<body>
    <div id="app">
        <button @click="getJoke">点我获取笑话哦</button>
        <h4 v-text="joke">{{ joke }}</h4>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
    <script>
        var app = new Vue({
            el: "#app",
            data: {
                joke: "很好笑的笑话在这里显示哦~"
            },
            methods: {
                getJoke: function(){
                    var that = this;
                    axios.get("https://autumnfish.cn/api/joke/list?num=1").then(function(response){
                        //无法通过 this 拿到 vue 实例 ---> 外部顶一个 that 拿到 this
                        that.joke = response.data.data[0];
                        console.log(response);
                    }, function(error){
                        this.joke = "获取笑话失败！";
                    });
                }
            }
        })
    </script>
</body>
</html>
```

### 天气预报案例

使用和风天气提供的接口查询天气：

- key：`6c96211350034c248d877862dde69121`

- 获取天气：https://devapi.qweather.com/v7/weather/now?location=101280606&key=6c96211350034c248d877862dde69121
- 获取`7`天天气：https://devapi.qweather.com/v7/weather/3d?location=101280606&key=6c96211350034c248d877862dde69121

- 获取地理`id`：https://geoapi.qweather.com/v2/city/lookup?key=6c96211350034c248d877862dde69121&range=cn&lang=zh&location=shenzhen ---> `location.name location.id`

- 获取天气生活指数：https://devapi.qweather.com/v7/indices/1d?location=101280606&key=6c96211350034c248d877862dde69121&type=1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16

  `lifeComfort:{comf:"舒适度",cw:"洗车",drsg:"穿衣",flu:"感冒",sport:"运动",trav:"旅游",uv:"紫外线",air:"空气污染扩散条件",ac:"空调开启",ag:"过敏",gl:"太阳镜",mu:"化妆",airc:"晾晒",ptfc:"交通",fsh:"钓鱼",spi:"防晒"}`

- 获取空气质量：https://devapi.qweather.com/v7/air/now?location=101280606&key=6c96211350034c248d877862dde69121

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>天知道案例</title>
      <link rel="stylesheet" href="./css/indexCool.css"/>
  </head>
  <body>
      <div class="warm" id="app">
          <div class="search_form">
              <div class="logo"><img src="./images/logo.png" alt="logo" /></div>
              <div class="form_group">
                  <input type="text" class="input_txt" v-model="city" @keyup.enter="queryWeather" placeholder="请输入要查询的天气"/>
                  <button class="input_sub" @click="queryWeather">搜索</button>
              </div>
              <div class="hotkey">
                  热门城市：
                  <a href="javascript:void(0);" v-for="(hotCity, index) in hotCitys" @click="searchThisCityWeather(hotCity)">{{ hotCity }}</a>
              </div>
          </div>
          <ul class="weather_list">
              <li v-for="(item, index) in forecastList" :style="{transitionDelay:index*100+'ms'}">
                  <div class="info_type">
                      <span class="iconfont" v-text="item.textDay"></span>
                  </div>
                  <div class="info_temp">
                      <b>低温 {{ item.tempMin }}℃</b>
                      ~
                      <b>高温 {{ item.tempMax }}℃</b>
                  </div>
                  <div class="info_date">
                      <span>{{ item.fxDate }}</span>
                  </div>
              </li>
          </ul>
      </div>
      <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
      <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
      <script>
          var app = new Vue({
              el: "#app",
              data: {
                  city: "",
                  cityId: 0,
                  forecastList: [],
                  hotCitys: ["北京", "上海", "广州", "杭州", "上海", "西安", "深圳", "南京"]
              }, methods: {
                  searchThisCityWeather:function(hotCity){
                      this.city = hotCity;
                      this.queryWeather();
                  },
                  queryWeather:function(){
                      this.forecastList = [];
                      var that = this;
                      console.log(this.city);
                      axios.get("https://geoapi.qweather.com/v2/city/lookup?key=6c96211350034c248d877862dde69121&range=cn&lang=zh&location="+this.city).then(function(response){
                          for(let i = 0; i < response.data.location.length; i++) {
                              if(response.data.location[i].name == that.city) that.cityId = response.data.location[i].id;
                          }
                      }, function(error){
                          alert("404!出错了，请联系管理员！！！");
                      });
                      setTimeout(function(){
                          axios.get("https://devapi.qweather.com/v7/weather/3d?key=6c96211350034c248d877862dde69121&location=" + that.cityId).then(function(response){
                              that.forecastList = response.data.daily;
                          }, function(error){
                              alert("404!出错了，请联系管理员！！！");
                          });
                      }, 200);
                  }
              }
          })
      </script>
  </body>
  </html>
  ```

## `Vue`综合应用

网页版音乐播放器

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="./musiccss/index.css"/>
    <title>音乐播放器</title>
</head>
<body>
    <div class="wrap">
        <div class="play_wrap" id="player">
            <!-- 搜索框 -->
            <div class="search_bar">
                <img src="./musicimages/player_title.png">
                <input v-model="query" type="text" autocomplete="off" @keyup.enter="searchMusic" @click="searchMusic">
            </div>
            <div class="center_con">
                <!-- 搜索结果 -->
                <div class="song_wrapper" ref="song_wrapper">
                    <ul class="song_list">
                        <!-- 遍历查询到的播放列表 -->
                        <li v-for="(music, index) in musicList">
                            <!-- 播放歌曲 -->
                            <a href="javascript:void(0);" @click="playMusic(music.id)"></a>
                            {{ music.name }}
                            <!-- 播放MV -->
                            <span>
                                <!-- MV 按钮，有 MV 才显示 -->
                                <i @click="playMV(music.mvid)" v-if="music.mvid != 0"></i>
                            </span>
                        </li>
                    </ul>
                    <!-- 播放列表和播放界面的分割线 -->
                    <img src="images/line.png" class="switch_btn" alt="">
                </div>
                <!-- 播放界面 -->
                <div class="player_con" :class="{playing:isPlay}">
                    <!-- 播放杆 -->
                    <img src="./musicimages/player_bar.png" class="play_bar">
                    <!-- 黑胶碟片 -->
                    <img src="/musicimages/disc.png" class="disc autoRotate" />
                    <!-- 碟片封面 随歌曲变化而变化 -->
                    <img :src="musicCover==''?'./musicimages/cover.png':musicCover" class="cover autoRotate">
                </div>
                <!-- 评论列表 -->
                <div class="comment_wrapper" ref='comment_wrapper'>
                    <!-- 黑胶碟片和留言分割线 -->
                    <img src="./musicimages/line.png" class="right_line">
                    <h5 class='title'>精选留言</h5>
                    <div class="comment_list">
                        <!-- 遍历留言 -->
                        <dl v-for="(hotComment, index) in hotComments">
                            <dt>
                                <img :src="hotComment.user.avatarUrl">
                            </dt>
                            <dd class="name">{{ hotComment.user.nickname }}</dd>
                            <dd class="detail">
                                {{ hotComment.content }}
                            </dd>
                        </dl>
                    </div>
                </div> 
            </div>
            <!-- 音乐播放底部 默认显示音乐而并不是MV -->
            <div class="audio_con">
                <audio ref='audio' @play="play" @pause="pause" :src="musicURL" controls autoplay loop class="myaudio"></audio>
              </div>
            <!-- MV播放底部 -->
            <div class="video_con" v-show="showVideo">
                <video ref='video' :src="mvURL" controls="controls"></video>
                <div class="mask" @click="closeMv"></div>
            </div>
        </div>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
    <script>
        //设置 axios 访问的基础 URL
        axios.defaults.baseURL = 'https://autumnfish.cn';
        var player = new Vue({
            el: "#player",
            data: {
                query: "",
                showVideo: false,
                musicList: [],
                hotComments: [],
                musicURL: "",
                mvURL: "",
                musicCover: "",
                isPlay: false
            },
            methods: {
                // 搜索功能 ---> 结果存储在 musicList 中 ---> 获取关键字使用 v-model ---> 如果关键字为空，不进行查询，直接返回
                searchMusic:function(){
                    if(this.query == "") return;
                    //箭头函数的 this 跟外层一致
                    axios.get("/search?keywords=" + this.query).then(response => {
                        this.musicList = response.data.result.songs;
                    });
                    this.query = "";
                },
                playMusic:function(musicId){
                    //获取这首歌曲进行播放 ---> 替换音乐播放底部 musicURL
                    axios.get("/song/url?id=" + musicId).then(response => {
                        this.musicURL = response.data.data[0].url;
                    })
                    //获取这首歌曲的封面 ---> 设置黑胶碟片的封面 
                    axios.get("/song/detail?ids=" + musicId).then(response => {
                        this.musicCover =  response.data.songs[0].al.picUrl;
                    });
                    //获取这首歌曲的精选留言 ---> 设置留言列表
                    axios.get('/comment/hot?type=0&id=' + musicId).then(response => {
                        this.hotComments = response.data.hotComments;
                    });
                },
                playMV:function(mvid){
                    if(mvid) {
                        this.showVideo = true;
                        axios.get('/mv/url?id=' + mvid).then(response => {
                            // 暂停歌曲播放
                            this.$refs.audio.pause();
                            // 获取mv地址
                            this.mvURL = response.data.data.url;
                        })
                    }
                },
                play:function(){
                    this.isPlay = true;
                    this.mvURL = "";
                },
                pause:function(){
                    this.isPlay = false;
                },
                closeMv:function(){
                    this.showVideo = false;
                    this.$refs.video.pause();
                }
            }
        })
    </script>
</body>
</html>
```