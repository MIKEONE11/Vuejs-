# Vuejs补充

# 1.邂逅Vuejs

![image-20221025201657999](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221025201657999.png)

- Vue 有很多特点和 Web 开发中很多常见的功能
  - 解耦视图和数据
  - 可复用的组件
  - 前端路由技术
  - 状态管理
  - 虚拟 DOM

## Vue.js 安装

#### 1.直接 CDN 引入

选择引入开发环境版本还是生产环境版本

- 开发环境版本（==Vue2 版本==）：

  <script src="https://cdn.jsdelivr.net/npm/vue@2.7.10/dist/vue.js"></script>



####  2.下载和引入

![image-20221025203029533](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221025203029533.png)

#### 3.NPM 安装

**后续通过 webpack 和 CLI 的使用**



## 体验Vuejs

```html
<div id="app">
    <h1>{{message}}</h1>
    <h5>{{name}}</h5>
</div>

<div>{{message}}</div>

<!--使用 CDN 方式引入 Vue-->
<script src="https://cdn.jsdelivr.net/npm/vue@2.7.10/dist/vue.js"></script>

<script>
    const app = new Vue({
      el: '#app',     				//用于挂载要管理的元素
      data: {         				//定义数据
        message: '你好',
        name: '李银河'  
      }
    })
  </script>
```

输出：![image-20221025212041922](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221025212041922.png)

### Vue列表显示

```js
<div id="app">
    <ul>
      <li v-for="item in movies">{{item}}</li>
    </ul>
  </div>
  <script src="../vue.js"></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        message: '你好',
        movies: ['海贼王', '海王', '星际穿越', '盗梦空间']
      }
    })
  </script>
```

输出：![image-20221025214035234](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221025214035234.png)

- 这种编程遵循的是响应式编程，当数据发生改变时，会自动追加元素到指定位置

  ![image-20221025214258693](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221025214258693.png)-- 控制台给列表追加元素，列表数据自动添加--![image-20221025214317952](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221025214317952.png)

### 实现计数器

```html
<div id="app">
    <h2>当前计数：{{counter}}</h2>
    <button v-on:click="add">+</button>		//v-on:click 绑定点击事件
    <button v-on:click="sub">-</button>
</div>

<script>
    const app = new Vue({
      el: '#app',
      data: {
        counter: 0
      },
      methods: {				//在 methods 内定义方法
        add: function() {
          this.counter++
        },
        sub: function () {
          this.counter--
        }
      }
    })
  </script>
```

实操：![image-20221026103350406](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026103350406.png)

**这里我们使用了新的 属性和新的指令：**

- methods 属性：用于在 Vue 对象中定义方法
- `v-on:click`指令(==语法糖：@click==)：用于监听某个元素的点击事件，并且需要指定当发生点击时，执行的方法



## Vue 中的 MVVM 

![image-20221026104131634](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026104131634.png)

![image-20221026104513947](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026104513947.png)

#### 创建 Vue 实例传入的 options

 <img src="C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026105151013.png" alt="image-20221026105151013" style="zoom: 67%;" />

> <font color=red>组件当中 data 必须是一个函数</font>



## Vue 的生命周期

![img](https://img-blog.csdnimg.cn/20190704110511249.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L09yaWdpbmFsbHlfTQ==,size_16,color_FFFFFF,t_70#pic_center)



# 2.Vue 基础语法

## 2.1插值语法

#### Mustache

- 使用 Mustache 语法（也就是双大括号）可以将 data 中的文本数据插入到 HTML 中

  > Mustache ：胡须/胡子

- 在 Mustache 中不仅可以写变量，也可以写一些简单的表达式

  ```html
  <div id="app">
      <p>{{firstName + ' ' + lastName}}</p>
      <h3>{{counter * 2}}</h3>
    </div>
    <script src="../vue.js"></script>
    <script>
      const app = new Vue({
        el: '#app',
        data: {
          firstName: 'Alan',
          lastName: 'Averson',
          counter: 100
        },
        methods: {}
      });
    </script>
  ```

  打印：![image-20221026114131966](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026114412010.png)

#### v-once指令

- 该指令后面不需要跟任何表达式，如：![image-20221026115424944](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026115424944.png)
- 该指令表示元素和组件只渲染一次，不会随着数据的改变而改变

```html
<div id="app">
    <h2>{{message}}</h2>
    <h2 v-once>{{message}}</h2>
</div>

<script>
const app = new Vue({
  el: '#app',
  data: {
    message: '你好啊'
  },
  methods: {}
});
</script>
```

打印：![image-20221026115120170](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026115120170.png)--改变message的数据--![image-20221026115151201](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026115151201.png)--<img src="C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026115301982.png" alt="image-20221026115301982"  />

#### v-html指令

- 可以解析出 Mustache 内的 html 标签

- 用法：

  ```html
  <div id="app">
      <h2 v-html="url"></h2>
    </div>
  
    <script>
      const app = new Vue({
        el: '#app',
        data: {
          url: '<a href="http://www.baidu.com">百度一下</a>'
        },
        methods: {}
      });
    </script>
  ```

  打印：![image-20221026120310032](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026120310032.png)

#### v-text 指令

v-text 作用和 Mustache 作用相似：都是用于将数据显示到页面中

```js
<h2 v-text="message"></h2>
<h2>{{message}}</h2>

const app = new Vue({
  el: '#app',
  data: {
    message: '你好'
  },
  methods: {}
});
```

打印：![image-20221026115120170](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026115120170.png)

> v-text 弊端：如果添加了该指令的元素内部有内容，那么 v-text 接的数据将会将内容覆盖

#### v-pre 指令

用于跳过这个元素和它子元素的编译过程，用于显示原本的 Mustache 语法

```js
<div id="app">
   <h2 v-pre>{{message}}</h2>
   <h2>{{message}}</h2>
</div>

const app = new Vue({
  el: '#app',
  data: {
    message: '你好'
  },
  methods: {}
});
```

打印：![image-20221026121246110](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026121246110.png)

#### v-cloak指令

![image-20221026121658722](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026121658722.png)

> cloak：斗篷



## 2.2绑定属性

#### v-bind介绍

除了内容需要动态来决定外，某些属性我也希望动态类绑定

- 比如动态绑定 a 标签的 href 属性
- 动态绑定 img 标签的 src 属性

这个时候，可以使用 v-bind 指令：

- 作用：动态绑定属性
- 语法糖： :

```html
<img v-bind:src="imgUrl" alt="" style="width: 50px; height: 50px">

<script>
    const app = new Vue({
      el: '#app',
      data: {
        imgUrl: 'https://v2.cn.vuejs.org/images/logo.svg'
      },
      methods: {}
    });
  </script>
```

打印：![image-20221026132302204](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026132302204.png)

#### v-bind 动态绑定 class

**绑定方式：**

**1.对象语法**

```html
<div id="app">
    <h2 :class="{active: isActive, line: isLine}">{{message}}</h2>
    <button @click="btnClick">点击</button>
</div>

<script>
    const app = new Vue({
      el: '#app',
      data: {
        message: '你好啊',
        isActive: false,
        isLine: false
      },
      methods: {
        btnClick: function() {
          this.isActive = !this.isActive
        }
      }
    });
  </script>
```

打印:![image-20221026171023720](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026171023720.png)

> 除了动态绑定 class，元素自己静态的class不会被覆盖

除了可以在元素内部使用确定class动态绑定的值，还可以在 method 内定义方法，在元素内部调用

```html
<div id="app">
    <h2 :class="getClasses()">{{message}}</h2>
    <button @click="btnClick">点击</button>
</div>

<script>
    const app = new Vue({
      el: '#app',
      data: {
        message: '你好啊',
        isActive: false,
        isLine: false
      },
      methods: {
        btnClick: function() {
          this.isActive = !this.isActive
        },
        getClasses: function() {
        	return {active: this.isActive, line: this.isLine}
        }
      }
    });
  </script>
```

打印时效果不变：![image-20221026171023720](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026171023720.png)

**2.数组语法：**

当类比较多时，可以使用数组语法

```html
<h2 :class="[active, line]">{{message}}</h2>
<script>
const app = new Vue({
  el: '#app',
  data: {
    message: '你好啊',
    active: 'aaa',
    line: 'bbb'
  },
  methods: {
  }
});
</script>
    
<!--或者在 methods 中定义-->
<h2 :class="getClasses()">{{message}}</h2>
<script>
const app = new Vue({
  el: '#app',
  data: {
    message: '你好啊',
    active: 'aaa',
    line: 'bbb'
  },
  methods: {
	 getClasses: function() {
        return [this.active, this.line]
    }
  }
});
</script>    
```

#### v-bind 绑定 style

1，绑定方式一：

![image-20221026174115922](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026174115922.png)

```js
<div id="app">
    <h2 :style="fontSize: finalSize + 'px'; backgroundColor: finalColor">{{message}}</h2>
</div>
<script src="../js/vue.js"></script>

<script>
const app = new Vue({
  el: '#app',
  data: {
    message: '你好啊',
    finalSize: 100,
    finalColor: red
  },
  methods: {}
});
</script>

<!--抽成方法-->
<div id="app">
    <h2 :style="getStyles()">{{message}}</h2>
</div>
<script src="../js/vue.js"></script>

<script>
const app = new Vue({
  el: '#app',
  data: {
    message: '你好啊',
      finalSize: 100,
      finalColor: red
  },
  methods: {
      getStyles: function() {
          return {fontSize: this.finalSize + 'px'; backgroundColor: this.finalColor}
      }
  }
});
</script>
```

2.绑定方式二：

![image-20221026174159000](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026174159000.png)

```
<div id="app">
    <h2 :style="[baseStyle, baseStyle1]">{{message}}</h2>
</div>
<script src="../js/vue.js"></script>

<script>
const app = new Vue({
  el: '#app',
  data: {
    message: '你好啊',
    baseStyle: {fontSize: '100px'},
    baseStyle1: {backgroundColor: 'red'}
  },
  methods: {}
});
</script>
```



## 2.3 计算属性

- 在模板中，我们可以通过插值语法显示一些 data 中的数据

- 但是有些情况，我们希望对数据进行一些转化后在显示，或者需要将多个数据结合起来进行显示
  - 比如我们有 firstName 和 lastName 两个名称变量，我们需要显示完整的名称
  - 但是如果多个地方都需要显示完整的名称，我们就需要多写几个{{firstName}} {{lastName}}

- 我们可以将上面的代码换称<font color=red>计算属性</font>:

  - 计算属性是写在 computed 中

  <img src="C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026181005429.png" alt="image-20221026181005429" style="zoom:80%;" /><img src="C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026180839440.png" alt="image-20221026180839440" style="zoom:80%;" />

打印：![image-20221026180850478](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026180850478.png)

> computed 内定义的同样是函数（本质上是属性），类似于 methods ，但是 **computed 内的函数的在使用时不用加 （）**；<font color=red>计算属性只会调用一次，但是 methods 会调用多次</font>
>
> 对于上述数据拼接的写法还可以使用 定义方法的形式
>
> ```html
> <div id="app">
>   <h2>{{getFullName}}</h2>
> </div>
> <script src="../vue.js"></script>
> <script>
> const app = new Vue({
>   el: '#app',
>   data: {
>     firstName: 'Alan',
>     lastName: 'Averson'
>   },
>   methods: {
>     getFullName: function() {
>         return this.firstName + ' ' + this.lastName
>     }  
>   }
> });
> </script>
> ```

#### 2.3.1 计算属性的复杂操作

需求：计算书的总价

```js
<div id="app">
    <h2>总价格：{{totalPrice}}</h2>
  </div>
  <script src="../vue.js"></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        books: [
          {id: 110, name: '十万个为什么', price: 102},
          {id: 111, name: '钢铁是怎样炼成的', price: 65},
          {id: 112, name: '海伦凯勒', price: 87},
          { id: 113, name: '活着', price: 25 },
        ]
      },
      computed: {
        totalPrice: function() {
          let price = 0
          for (let i in this.books) {
            price += this.books[i].price
          }
          return price
        }
      }
    });
  </script>
```

打印：![image-20221026183254936](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026183254936.png)

#### 2.3.2 计算属性的 setter 和 getter

- 每个计算属性都包含了 一个 setter 和 一个 getter

  - 在前面的例子中，我们只是用 getter 来读取

    > 一般情况下我们只需要实现 getter 方法。而不用实现 setter 方法；
    >
    > ```html
    > <h2>{{fullName}}</h2>
    > <script>
    > data: {
    >     firstName: 'Alan',
    >     lastName: 'Averson'
    >   },
    >   computed: {
    >     fullName: {
    >       //计算属性一般是没有 set 方法，这时候就是一个只读属性    
    >       get: function() {
    >         return this.firstName + ' ' + this.lastName
    >       }
    >       // 所以一般只写成下面的形式，这也验证了为什么使用计算属性时不用()
    >       // fullName: function () {
    >       //   return this.firstName + ' ' + this.lastName
    >       // }  
    >     }
    >   }
    > </script>    
    > ```
    >
    > 打印：![image-20221026180850478](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026180850478.png)

  - 在某些情况下，也可以提供一个 setter 方法（不常用）

  - 在需要写 setter 的时候，代码如下：

    ```js
    <div id="app">
        <h2>{{fullName}}</h2>
      </div>
      <script src="../vue.js"></script>
      <script>
        const app = new Vue({
          el: '#app',
          data: {
            firstName: 'Alan',
            lastName: 'Averson'
          },
          computed: {
            fullName: {
              set: function(newValue) {
                const names = newValue.split(' ')
                this.firstName = names[0]
                this.lastName = names[1]
              } ,
              get: function() {
                return this.firstName + ' ' + this.lastName
              }
            }
          }
        });
      </script>
    ```

    修改app.fullName 的值：![image-20221026213943396](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026213943396.png)![image-20221026213955308](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026213955308.png)

#### 2.3.3 计算属性 和 methods 对比

- **使用 methods**

```html
<div id="app">
    <h2>{{fullName()}}</h2>
    <h2>{{fullName()}}</h2>
    <h2>{{fullName()}}</h2>
    <h2>{{fullName()}}</h2>
</div>
  <script src="../vue.js"></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        firstName: 'Alan',
        lastName: 'Averson'
      },
      methods: {
        getFullName: function() {
            
          return this.firstName + ' ' + this.lastName
        }
      }
</script>
```

显示和输出：<img src="C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026214951214.png" alt="image-20221026214951214" style="zoom:50%;" /> 后台调用四次：![image-20221026215003903](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026215003903.png)

- **使用 计算属性**

```
<div id="app">
    <h2>{{fullName}}</h2>
    <h2>{{fullName}}</h2>
    <h2>{{fullName}}</h2>
    <h2>{{fullName}}</h2>
  </div>
  <script src="../vue.js"></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        firstName: 'Alan',
        lastName: 'Averson'
      },
      computed: {
        fullName: function () {
          console.log('fullName');
          return this.firstName + ' ' + this.lastName 
        }
      }
    });
  </script>
```

显示和输出：<img src="C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026214951214.png" alt="image-20221026214951214" style="zoom:50%;" /> 后台调用一次：![image-20221026215150212](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026215150212.png)

> 由上述小案例可知，计算属性只会执行一次代码，而 methods 会执行多次，所以计算属性的性能要比使用 methods 的高



## 2.4 事件监听

#### v-on 介绍

作用：绑定事件监听器

语法糖：@

预期：Function | Inline Statement | Object

参数：event

```html
<div id="app">
    <h3>{{counter}}</h3>
    <button @click="increment()">+</button>
    <button @click="decrement()">-</button>
</div>
<script>
    data: {
        counter: 0
      },
    methods: {
      increment() {
        this.counter++
      },
      decrement() {
        this.counter--
      }
    }
</script>
```

实现：![image-20221026223834397](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026223834397.png)

#### v-on 参数传递的问题

- 当通过 methods 中定义方法，以供 @click 调用时，需要注意参数问题

  - 如果方法不需要额外参数，调用方法时方法名后面可不加（）

  - 如果定义的方法本身有一个参数，而调用时没有写（），那么会默认将原生事件 event 参数传递进去

     ![image-20221026225209861](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026225209861.png)![image-20221026225132704](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026225132704.png)

    控制台输出：![image-20221026225242176](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026225242176.png)

  - 如果需要同时传入某个参数，同时需要 event 时，可以通过 $event 传入事件

     ![image-20221026225755790](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026225755790.png)<img src="C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026225818590.png" alt="image-20221026225818590" style="zoom:80%;" />

    控制台输出：![image-20221026225907678](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026225907678.png)



#### v-on 的修饰符

**.stop 修饰符**：

调用event.stopPropagation()，可用于阻止事件冒泡

![image-20221026230656561](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026230656561.png)

![image-20221026230712399](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026230712399.png)

![image-20221026230756075](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026230756075.png)

点击按钮打印：![image-20221026230808657](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026230808657.png)



**.prevent 修饰符**：

调用event.preventDefault()，阻止默认行为

- 比如表单点击提交会默认跳转到指定页面，使用.prevent修饰符即可阻止这一默认行为

  ![image-20221026231805409](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026231805409.png)![image-20221026231819398](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026231819398.png)

  点击提交按钮==不会跳转==并且打印内容：![image-20221026231855811](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026231855811.png)



**.keyCode|.keyAlias**：只当事件是从特定键触发时才会触发回调

![image-20221026232424766](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026232424766.png)![image-20221026232437937](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026232437937.png)

当键盘被抬起时，就触发一次keyUp事件：![image-20221026232723936](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026232723936.png)![image-20221026232626576](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221026232709707.png)

监听某个键的抬起：![image-20221027101202253](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027101202253.png)



**.native 修饰符**：监听组件根元素的原生事件

**.once 修饰符**：

只触发一次回调，如按钮添加点击事件，加上 .once 修饰符后只允许点击一次



## 2.5条件渲染

#### 条件渲染：

**v-if 和 v-else：**

```html
<div id="app">
    <h2 v-if="status">{{message}}</h2>
    <h2 v-else>{{name}}</h2>
  </div>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        message: '你好',
        name: '李银河',
        status: true
      },
      methods: {}
    });
  </script>
```

显示：![image-20221027110043777](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027110043777.png)修改status 为 false：![image-20221027110136285](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027110136285.png)

**v-else-if：**

 ![image-20221027110747130](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027110747130.png)输出：![image-20221027110823995](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027110823995.png)



##### v-if 和 v-else 小案例：

```html
<div id="app">
    <span v-if="inputShow">
      <label for="username">用户帐号</label>
      <input type="text" id="username" placeholder="用户帐号">
    </span>
    <span v-else>
      <label for="useremail">用户邮箱</label>
      <input type="text" id="useremail" placeholder="用户邮箱">
    </span>
    <button @click="inputShow = !inputShow">切换</button>
  </div>
  <script src="../vue.js"></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        inputShow: true
      }
    });
  </script>
```

点击切换前：![image-20221027112717283](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027112717283.png)点击切换后:![image-20221027112647873](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027112647873.png)

**案例问题**：当在用户帐号输入框的时候，输入内容，并点击切换按钮，内容不消失

-  切换前：![image-20221027112953352](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027112953352.png)

- 切换后：![image-20221027113035717](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027113035717.png)

**解决方案：**在 input 框内==添加 key 字段==

<img src="C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027113257560.png" alt="image-20221027113257560" style="zoom:80%;" />

-  切换前：![image-20221027112953352](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027112953352.png)
- 切换后：![image-20221027113231894](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027113231894.png)



#### v-show

v-show 和 v-if 非常类似，可以决定元素是否显示

```html
<div id="app">
    <h2 v-if="isShow">{{message}}</h2>
    <h2 v-show="isShow">{{message}}</h2>
  </div>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        message: '你好',
        isShow: true
      },
    });
  </script>
```

演示：![image-20221027114153494](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027114153494.png)  修改app.isShow = false：![image-20221027114253425](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027114253425.png)

> 上述例子可知：
>
> ==当条件为 false 时，v-if 便不会存在 dom中；而v-show 只是给我们的元素添加了一个行内样式 display:none==
>
> 当需要在显示和隐藏之间前换频率非常高时，使用 v-show ，当只切换一次时，使用 v-if



## 2.6 循环遍历

#### v-for 遍历数组的使用：

```html
<div id="app">
    <ul>
      <li v-for="item in names">{{item}}</li>
    </ul>
  </div>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        names: ['莱昂纳多','陈晓','艾弗森','小罗伯特']
      },
      methods: {}
    });
  </script>
```

显示：![image-20221027115503369](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027115503369.png)

**需求：在遍历的过程中，获得索引值**

![image-20221027121518970](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027121518970.png)

输出：![image-20221027121531292](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027121531292.png)

#### v-for 遍历对象的使用：

![image-20221027122305112](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027122305112.png)

输出：![image-20221027122316045](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027122316045.png)

> （）内第一个参数就是值，第二个参数是键
>
> 获取对象同时也可以获取到对应的索引，格式 `(value, key, index) in obj`



#### 哪些数组的方法是响应式的

**puch()**：数组末尾添加一个或多个元素

![image-20221027124254043](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027124254043.png)![image-20221027124304276](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027124304276.png)

 ![image-20221027124320221](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027124320221.png)	点击按钮后：![image-20221027124343237](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027124343237.png)

**pop()**：删除数组最后一个元素

![image-20221027124512448](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027124512448.png)

 ![image-20221027124320221](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027124320221.png)	点击按钮后：![image-20221027124714706](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027124714706.png)

**shift()**：删除数组第一个元素

**unshift()**：在数组末尾最前面添加于元素

**splice()**：

作用：删除元素/ 替换元素 / 插入元素

参数：

- 删除元素：第一个参数为从索引为几的元素开始删除，第二个参数为要删除的个数

- 替换元素：第一个参数为从索引为几的元素开始替换，第二个参数表示替换几个元素，第三个开始表示要替换的元素

  ![image-20221027130110875](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027130110875.png)

  输出：![image-20221027124320221](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027124320221.png) 点击按钮后：![image-20221027130511878](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027130511878.png)

- 插入元素：第一个参数为从索引为几的元素开始插入，第二个参数为0，第三个开始表示要插入的元素

**sort()**：对数组进行排序

**reverse()**：对数组进行反转

> 注意：通过索引值修改数组的元素无法做到响应式改变页面数据
>
> 如：![image-20221027131226156](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027131226156.png)这种方式不会有响应式的数据变化，可以用splice() 方法代替：
>
> ![image-20221027131425508](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027131425508.png)
>
> 还有一种方法就是使用 vue 内部实现的方法：![image-20221027131615413](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027131615413.png)



## 2.7阶段案例

#### 案例一：

初始时第一个 li 为红色，当点击哪个 li 时，该 li 变成红色 

```html
<div id="app">
    <ul>
      <li 
      v-for="(item, index) in movies" 
      :class="{active: currentIndex == index}"
      @click="getClick(index)">{{item}}</li>
    </ul>
  </div>

  <script>
    const app = new Vue({
      el: '#app',
      data: {
        movies: ['海贼王', '加勒比海盗', '海伦凯勒', '海尔兄弟'],
        currentIndex: 0
      },
      methods: {
        getClick(index) {
          this.currentIndex = index
        }
      }
    });
  </script>
```

![image-20221027134221559](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027134253049.png) ![image-20221027134306610](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027134306610.png)

#### 案例二：

> ==E:/CODE/Vue_Code/书籍购物车==



## 2.8JavaSript 高阶函数的使用

#### 1.filter() ：

filter() 函数内传入一个回调函数，这个函数必须返回一个布尔值

- 当返回 true 时：函数内部会自动将这次回调的 n 加入到新的数组中
- 当返回 false 时：函数内部会过滤掉这次的 n

```js
//打印 nums 数组中小于100的元素
const nums = [12, 143, 54, 43, 367, 102, 29]

let newNums = nums.filter(function(n) {
    return n < 100
})
console.log(newNums)	//--[12, 54, 43, 29]
```

#### 2.map()：

```js
//将 newNums 中的元素乘以2后返回一个新的数组
const newNums = [12, 54, 43, 29];

let new2Nums = newNums.map(function(n) {
    return n * 2
})
console.log(new2Nums)	//--[24, 108, 86, 58]
```

#### 3.reduce()：

reduce() 函数可对数组中所有的内容进行汇总

reduce() 函数内传入两个参数

参数一：回调函数，函数内传入两个参数，第一个为 previous（函数体上一次返回的值） ，第二个就是数组依次传入的元素

参数二：数值（作为函数体返回的初始值）

```js
const new2Nums = [24, 108, 86, 58]
let totalNums = new2Nums.reduce((previous, n) => {
	return previous + n
}, 0)
console.log(totalNums)	//-- 276
```



## 2.9表单绑定 v-model 

- 表单控件在实际开发中是非常罕见的。特别是对于用户信息的提交，需要大量的表单

- Vue 中使用 v-model 指令来实现表单元素和数据的双向绑定

  ```js
  <div id="app">
      <input type="text" v-model="message">
      {{message}}
    </div>
  
    <script>
      const app = new Vue({
        el: '#app',
        data: {
          message: '你好啊'
        },
        methods: {}
      });
    </script>
  ```

  输出：![image-20221027164931238](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027164931238.png)

​		在控制台修改 message 的值，表单的值会随之改变：![image-20221027174042840](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027174042840.png)

​		而修改表单内的值时， message 的值也会随之修改，这就是双向绑定；

​		修改表单内的值：![image-20221027174221911](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027174221911.png)

### v--model 原理：

v-model 其实是一个语法糖，它的背后其实进行了两个操作：

1. v-bind 绑定一个 value 属性
2. v-on 指令给当前元素绑定 input 事件

```html
<input type="text" :value="message" @input="message = $event.target.value">
```

上述写法就是 v-model 实现表单数据双向绑定的完整写法

### v-model 结合 radio：

```js
<div id="app">
    <label for="male">
      <input type="radio" id="male" value="男" v-model="sex">男
    </label>
    <label for="female">
      <input type="radio" id="female" value="女" v-model="sex">女
    </label>
  </div>

  <script>
    const app = new Vue({
      el: '#app',
      data: {
        sex: ''
      }
    });
  </script>
```

这里动态绑定了 sex 的值，点击哪个单选框，对应的 value 值就会赋给 sex；

添加了 v-model 的表单不需要添加 name 属性对两个表单进行互斥操作

> 给 radio 设置默认值：![image-20221027180710421](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027180710421.png)现在单选框value 为男的单选框就默认被勾选了

### v--model 结合 checkbox

#### checkbox 单选框：

```html
<div id="app">
    <label for="agree">
      <input type="checkbox" id="agree" v-model="isAgree">同意协议
    </label>
    <br><br>
    <button :disabled="!isAgree">下一步</button>
  </div>

  <script>
    const app = new Vue({
      el: '#app',
      data: {
        message: '',
        isAgree: false
      }
    });
  </script>
```

演示：![image-20221027181752389](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027181752389.png)	点击同意：![image-20221027181812415](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027181812415.png)

**checkbox 复选框：**

```js
<div id="app">
    <input type="checkbox" value="篮球" v-model="hobbies">篮球
    <input type="checkbox" value="足球" v-model="hobbies">足球
    <input type="checkbox" value="羽毛球" v-model="hobbies">羽毛球
    <input type="checkbox" value="排球" v-model="hobbies">排球
    <h2>您的爱好是：{{hobbies}}</h2>
  </div>

  <script>
    const app = new Vue({
      el: '#app',
      data: {
        hobbies: []
      }
    });
  </script>
```

演示：![image-20221027182410608](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027182410608.png)

> ==单选框使用 v-model 绑定的是一个布尔值，复选框使用 v-model 绑定的则是一个数组==

### v-model 结合 select

- **select 单选**

```html
<div id="app">
    <select name="" id="" v-model="fruits">
      <option value="苹果">苹果</option>
      <option value="香蕉">香蕉</option>
      <option value="鸭梨">鸭梨</option>
      <option value="榴梿">榴梿</option>
    </select>
  </div>

  <script>
    const app = new Vue({
      el: '#app',
      data: {
        fruits:'苹果'
      }
    });
  </script>
```

打印：![image-20221027183141669](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027183141669.png)

- **select 多选**

```html
<div id="app">
    <select name="abc" id="" v-model="fruits" multiple>
      <option value="苹果">苹果</option>
      <option value="香蕉">香蕉</option>
      <option value="鸭梨">鸭梨</option>
      <option value="榴梿">榴梿</option>
    </select>
    {{fruits}}
  </div>

  <script>
    const app = new Vue({
      el: '#app',
      data: {
        fruits: []
      }
    });
  </script>
```

演示：![image-20221027183647639](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027183647639.png)

### 值绑定

![image-20221027184215926](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027184215926.png)

![image-20221027184142836](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027184142836.png)

演示：**![image-20221027184234519](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027184234519.png)**

### 修饰符

![image-20221027184410138](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221027184410138.png)

- **.lazy 修饰符：**当不想要表单内的数据跟 v-model 绑定的data中的数据==实时==响应时，使用 .lazy 修饰符即可实现，而只需表单失去焦点或者按下 enter键 v-model 绑定的data中的数据才变化

​	

# 3.组件化开发

## 认识组件化

![image-20221028104224076](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221028104224076.png)

### Vue 组件化思想

- 组件化是Vuejs重要思想

  - 它提供了一种抽象，让我们可以开发出一个个独立可复用的小组件来构造我们的应用

  - 任何的应用都回抽象成一棵组件树

    ![image-20221028104552293](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221028104552293.png)



## 组件化基础

### 1.注册组件

#### 注册组件的基本步骤

**组件的使用分成<font color=red>三个步骤：</font>**

- <font color=blue>创建组件构造器</font>
- <font color=blue>注册组件</font>
- <font color=blue>使用组件</font>

调用 Vue.extend()方法<font color=red>创建组件构造器</font>—>调用男Vue.component()方法<font color=red>注册组件</font>—>在Vue实例范围内<font color=red>使用组件</font>	

#### 组件化的基本使用

如下述三步骤：

```html
<div id="app">
   <!-- 3.使用组件 -->
   <my-cpn></my-cpn>
</div>

<script>
    
    // 1.创建组件构造器对象
    const cpnC = Vue.extend({
      template: `
        <div>
          <h2>我是标题</h2>
          <p>我是内容哈哈哈哈哈</p>
          <p>我是内容呵呵呵呵呵</p>
        </div>
      `
    })
    
    // 2.注册组件(全局组件)
    Vue.component('my-cpn', cpnC)

    const app = new Vue({
      el: '#app',
      data: {}
    });
</script>
```

打印：![image-20221028111115094](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221028111115094.png)

**使用组件时可多次使用，如:**

```html
<!-- 3.使用组件 -->
<my-cpn></my-cpn>
<my-cpn></my-cpn>
<my-cpn></my-cpn>
```

打印：![image-20221028111245675](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221028111245675.png)



#### 注册组件步骤解析

**1.Vue.extend()：**

- 调用Vue.extend() 创建的是一个组件构造器
- 通常在创建组件构造器时，传入一个 template 代表我自定义的组件模板
- 该模板就是在使用到组件的地方，要显示的 HTML 代码
- 事实上，这种写法在 Vue2.x 的文档中几乎已经看不到了，会直接时使用下面讲到的语法糖

**2.Vue.component()：**

- 调用 Vue.component() 是将刚才的组件构造器注册为一个组件，并且给它起一个组件的标签名
- 所以需要传递两个参数：1.注册组件的标签名 2.组件构造器

**3.**组件必须挂载在某个Vue 实例上，否则它不会生效



#### 全局组件和局部组件

##### 全局组件：

**上述注册的组件是全局组件，即：**

```js
// 注册组件(全局组件)
Vue.component('my-cpn', cpnC)
```

- 全局组件意味着可以在多个Vue的实例下面使用

  - 如果创建一个以上的Vue实例，那么在这些Vue实例挂载的元素内都可以使用全局注册的组件

  ```html
  <div id="app">
      <my-cpn></my-cpn>
  </div>
  
  <div id="app2">
      <my-cpn></my-cpn>
  </div>
  
  <script>
      
      // 注册组件(全局组件)
  	Vue.component('my-cpn', cpnC)
      
      //Vue实例1
      const app = new Vue({
        el: '#app',
        data: {
          message: ''
        },
        methods: {}
      })
  
      //Vue实例2
      const app2 = new Vue({
        el: '#app2',
        data: {
          message: ''
        },
        methods: {}
      })
  </script>
  ```

##### 注册局部组件：

<font color=red>在Vue 实例内部通过 components 注册的就是局部组件</font>

局部组件不会在别的 Vue实例挂载的元素上被使用

```js
const app = new Vue({
  el: '#app',
  data: {
    message: ''
  },
  components: {
    //cpn 使用组件时的标签名
    cpn: cpnC		//局部组件
  }  
})
```



#### 父组件和子组件

```html
<div id="app">
    <cpn2></cpn2>
  </div>

  <script>
    // 1.创建组件构造器1（子组件）
    const cpnC1 = Vue.extend({
      template: `
        <div>
          <h2>我是标题1</h2>
          <p>我是内容，哈哈哈</p>
        </div>
      `
    })

    // 1.创建组件构造器2（父组件）
    const cpnC2 = Vue.extend({
      template: `
        <div>
          <h2>我是标题2</h2>
          <p>我是内容，呵呵呵</p>
          <cpn1></cpn1>
        </div>
      `,
      components: {       //将子组件注册到父组件的components 内
        cpn1: cpnC1
      }
    })

	//root 组件
    const app = new Vue({
      el: '#app',
      data: {
        message: ''
      },
      components: {
        cpn2: cpnC2    //将父组件注册在Vue实例内的components内
      }
    });
  </script>
```

> ==注意点：==
>
> - 父组件注册到Vue实例内的 components 内
>
> - 子组件注册到父组件的 component 内
>
> - 在Vue实例挂载的 app节点内如果要使用**子组件**， 必须在 Vue实例的components 内也注册好才可以使用
>
>    ![image-20221028121922595](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221028121922595.png)![image-20221028121954046](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221028121954046.png)
>
>   - 因为当子组件注册到父组件的 components 时，Vue会编译好父组件的模板
>   - 该模板的内容已经决定了父组件将要渲染的 HTML (相当于父组件中已经有子组件)
>   - <child-cpn></child-cpn>是只能在父组件中被识别



#### 注册组件语法糖

##### 注册全局组件语法糖：

```html
<div id="app">
   <!-- 3.使用组件 -->
   <my-cpn></my-cpn>
</div>

<script>
    
    // 1.创建组件构造器对象
    const cpnC = Vue.extend()
    
    // 2.注册组件(全局组件)
    Vue.component('my-cpn', {
      template: `
        <div>
          <h2>我是标题</h2>
          <p>我是内容哈哈哈哈哈</p>
          <p>我是内容呵呵呵呵呵</p>
        </div>
      `
    })

    const app = new Vue({
      el: '#app',
      data: {}
    });
</script>
```

##### 注册局部组件语法糖：

```html
<div id="app">
   <!-- 3.使用组件 -->
   <my-cpn></my-cpn>
</div>

<script>
    
    // 1.创建组件构造器对象
    const cpnC = Vue.extend()
    
    const app = new Vue({
      el: '#app',
      data: {},
      components: {
        //2.注册局部组件  
      	my-cpn: {
          template: `
        	<div>
              <h2>我是标题</h2>
              <p>我是内容哈哈哈哈哈</p>
              <p>我是内容呵呵呵呵呵</p>
            </div>
      	`
      	} 
      }
    });
</script>
```

> 使用语法糖的形式注册组件，创建组件构造器的步骤可以省略
>
> ```js
> const cpnC = Vue.extend()   //这一步可省略
> ```



#### 模板的分离写法

如果我们能将 template 模块内的 HTML 分离出来写，然后挂载到对应组件上，会使结构变的非常清晰

Vue 提供了两种方案来定义 HTML 模块内容

**方法1:  通过 <font color=red>script</font> 标签，但是类型必须是 `text/x-template`**

- 在 body 标签内定义 script 标签，类型为 text/x-template，同时通过 **id属性** 绑定与注册的组件进行绑定2

```html
<div id="app">
    <cpn></cpn>
  </div>

  <!-- 使用 script 标签，类型为text/x-template -->
  <script type="text/x-template" id="cpn">
    <div>
      <h2>我是标题</h2>
      <p>我是内容哈哈哈哈哈</p>
    </div>
  </script>

  <script>

    // 注册一个全局组件
    Vue.component('cpn',{
      template: '#cpn'
    })

    const app = new Vue({
      el: '#app'
    });
  </script>
```

打印：![image-20221028134723486](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221028134723486.png)

**方法2：  使用 template 标签**

- 在 body 标签内定义 template 标签，通过 id属性 与注册的组件进行绑定


```html
<div id="app">
    <cpn></cpn>
  </div>

   <!-- 使用 template 标签 -->
  <template id="cpn">
    <div>
      <h2>我是标题</h2>
      <p>我是内容哈哈哈哈哈</p>
    </div>
  </template>

  <script>

    // 注册一个全局组件
    Vue.component('cpn',{
      template: '#cpn'
    })

    const app = new Vue({
      el: '#app'
    });
  </script>
```

打印：![image-20221028134723486](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221028134723486.png)



#### 组件的其他属性

##### 组件可以访问 Vue 实例数据吗？

<font color=red>组件内部是不能直接访问 Vue实例里面的数据的</font>,比如下面的写法：

![image-20221028140856994](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221028140856994.png)![image-20221028140910901](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221028140910901.png)



##### 组件数据的存放

组件是一个单独的功能模块的封装：

- 这个模块有属于自己的 HTML 模板，也应该有属于自己的数据 data

- 组件中的数据保存在 Vue.component 内的 data中，并且这个data不像 Vue实例中的是一个对象类型，<font color=red>组件中保存数据的 data 是一个**函数**类型，该函数内还必须返回一个对象</font>，而数据就保存在return内的这个对象中，如下图：

  ![image-20221028141837003](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221028141837003.png)![image-20221028140856994](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221028140856994.png)

  打印：![image-20221028134723486](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221028134723486.png)

#####  组件中的 data 为什么是函数？

**如果data是一个对象则会造成数据共享**
vue中组件是用来复用的，为了防止data复用，将其定义为函数。

如果 **data 不是函数**：
在多次使用该组件时，改变其中一个组件的值会影响全部该组件的值。
而如果是通过函数的形式返回出一个对象的话，在每次使用该组件时返回出的对象的地址指向都是不一样的，这样就能让各个组件的数据独立。

如果 **data 是函数**：
data数据是相互隔离，互不影响的，组件每复用一次，data数据就应该被复制一次，之后，当某一处复用的地方组件内data数据被改变时，其他复用地方组件的data数据不受影响，就需要通过data函数返回一个对象作为组件的状态。
通过函数的形式返回出一个对象的话，在每次使用该组件时返回出的对象的地址指向都是不一样的，这样就能让各个组件的数据独立，让各个组件实例维护各自的数据。

当我们将组件中的data写成一个函数，数据以函数返回值形式定义，这样每复用一次组件，就会返回一份新的data，拥有自己的作用域，类似于给每个组件实例创建一个私有的数据空间，让各个组件实例维护各自的数据。

组件的date单纯的写成对象形式，这些实例用的是同一个构造函数，由于JavaScript的特性所导致，所有的组件实例共用了一个data，就会造成一个变了全都会变的结果。

**为什么new Vue这个里面的data可以放一个对象？**
因为这个类创建的实例不会被复用。它只会new一次，不用考虑复用。

### 2.数据传递

#### 父子组件的通信

![image-20221030122634716](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221030122634716.png)

**前面提到子组件是不能直接引用父组件或者 Vue 实例的数据的**

但是在开发中，往往一些数据确实需要从上层传递到下层：

- 比如在一个页面中，我们从服务器请求到了很多数据
- 其中一部分数据，并非是我们整个页面的大组件来展示，而是需要下面的子组件来展示
- 这个时候，并不会让子组件再次发送一个网络请求，而是让**大组件（父组件）**将数据传递给**小组件（子组件）**

如何进行父子组件间的通信呢？

- <font color=red>通过 **props** 向子组件传递数据</font>
- <font color=red>通过**自定义事件**向父组件发送信息</font>

##### 父传子：Props 基本用法

- 在组件中，使用选项 props 来声明需要从父级接收到的数据

- props的值有两种方式：

  - 方式一：字符串数组，数组中的字符串就是传递时的名称 (**不常用**)

    ```js
    <div id="app">
        <cpn :cmovies="movies" :cmessage="message"></cpn>
      </div>
    
      <template id="cpn">
        <div>
          <ul>
            <li v-for="item in cmovies">{{item}}</li>
          </ul>
          <h4>{{cmessage}}</h4>
        </div>
      </template>
    
      <script>
        
    
        const app = new Vue({
          el: '#app',
          data: {
            message: '你好哦',
            movies: ['海贼王', '海尔兄弟', '海王']
          },
          components: {
            cpn： {
          		template: '#cpn',
         		props: ['cmovies', 'cmessage']
       		}
          }
        });
      </script>
    ```

    打印：![image-20221029151303054](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221029151303054.png)

  - 方式二：对象类型，对象可以设置传递时的类型，也可以设置默认值

    ```js
    //类型限制：规定了传入值的类型
    props: {
    	cmovies: Array,
    	cmessage: String
    }
    ```

    ```js
    
    //提供一些默认值，以及必传值
    components{		//全局组件
        template: '#cpn',
        props: {
            cmessage: {
                type: String,
                default: '哈哈哈',
                required: true
            }
    	}
    }
    ```

    > 注意点：
    >
    > 1.props 为对象类型的情况下，props 的某个属性如上面的cmessage传了一个<font color=blue>required必传值</font>，那么如果使用该组件时没有绑定这个属性则会**报错**：如下情况
    >
    >  <img src="C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221029154250674.png" alt="image-20221029154250674" style="zoom:67%;" />
    >
    > <img src="C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221029154338361.png" alt="image-20221029154338361" style="zoom:80%;" />
    >
    > 2.如果给 props 的某个属性传入了 <font color=red>default</font>，在使用组件时没有绑定该属性，则最终效果会显示 default 的默认值
    >
    > ![image-20221029155508090](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221029155508090.png)
    >
    > ![image-20221029155536017](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221029155536017.png)
    >
    > 打印：![image-20221029155617367](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221029155617367.png)
    >
    > 3.如果 props 的某个属性是对象或者数组类型，<font color=red>**default**（默认值）必须是一个函数</font>
    >
    > ![image-20221030094818752](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221030094818752.png)

##### props驼峰标识

在使用组件的时候，动态绑定的 props 属性命名**不要**使用驼峰标识法，否则会无法传递到父组件的数据；定义组件模板的时候可以使用驼峰标识法

![image-20221030100057865](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221030100057865.png)

但是可以使用 - 分隔：![image-20221030100206221](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221030100206221.png)

##### 子传父：自定义事件

**什么时候需要自定义事件呢？**

- 当子组件需要向父组件传递数据，就要用到自定义事件了
- v-on 不仅仅可以用于监听 DOM 事件，也可以用于组件间的自定义事件

**自定义事件的流程：**

- 在子组件中，通过 $emit() 来触发事件

  ![image-20221030104802992](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221030104802992.png)

- 在父组件中，通过 v-on 来监听子组件事件

  ![image-20221030104823360](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221030104823360.png)

```html
  <div id="app">
    <!-- 父组件接收子组件的自定义事件 -->
    <cpn @item-click="cpnClick"></cpn>
  </div>

  <template id="cpn">
    <div>
      <button v-for="item in categories" 
              @click="btnClick(item)">
        {{item.name}}
      </button>
    </div>
  </template>

  <script>

    const cpn = {
      template: '#cpn',
      data() {
        return {
          categories: [
            {id: '11', name: '精品推荐'},
            {id: '12', name: '手机数码'},
            {id: '13', name: '母婴推荐'},
            { id: '14', name: '秋季促销' },
          ]
        }
      },
      methods: {
        btnClick(item) {
          //emit:发射；
          // 子组件注册一个自定义事件 itemClick
          // item 为自定义事件的参数
          this.$emit('item-click', item)
        }
      }
    }

    const app = new Vue({
      el: '#app',
      data: {
        message: ''
      },
      components: {
        cpn
      },
      methods: {
        cpnClick(item) {
          console.log('cpnClick',item);
        }
      }
    });
  </script>
```

演示：![image-20221030123159153](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221030123159153.png)

> ==小案例：子传父实现计数器==
>
> ```html
>   <div id="app">
>     {{total}}
>     <!--发生两个事件，调用同一个函数  -->
>     <cpn @btnincre="cpntotal" @btndecre="cpntotal"></cpn>
>   </div>
> 
>   <template id="cpn"> 
>     <div>  
>       <br>
>       <button @click="increment">+</button>
>       <button @click="decrement">-</button>
>     </div>
>   </template>
> 
>   <script>
>     const app = new Vue({
>       el: '#app',
>       data: {
>         message: '',
>         total: 0
>       },
>       components: {
>         cpn: {
>           template: '#cpn',
>           data() {
>             return {
>               counter: 0
>             }
>           },
>           methods: {
>             increment() {
>               this.counter++
>               this.$emit('btnincre', this.counter)
>             },
>             decrement() {
>               this.counter--
>               this.$emit('btndecre', this.counter)
>             }
>           }
>         }
>       },
>       methods: {
>         cpntotal(counter){
>           this.total = counter
>         }
>       }
>     });	
>  </script>     
> ```
>
> 演示：![image-20221030122314596](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221030122314596.png)    按加号按钮：![image-20221030122238658](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221030122238658.png)按减号按钮：![image-20221030122334436](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221030122334436.png)

**补充**：父组件的数据传递给子组件，子组件最好<font color=red>避免使用如表单双向绑定的方式**直接修改** props 的数据</font>，而是在子组件的 data 中，将 props 中的数据赋值给一个新的变量

![image-20221030165317157](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221030165317157.png)



==组件通信案例：表单数据绑定==

```html
<div id="app">
    <cpn  :cnum1="num1" 
          :cnum2="num2"
          @num1change="num1change"
          @num2change="num2change"></cpn>
  </div>

  <template id="cpn">
    <div>
      <h2>props:{{cnum1}}</h2>
      <h2>data:{{dnum1}}</h2>
      <!-- <input type="text" v-model="dnum1"> -->
      <input type="text" :value="dnum1" @input="num1Input">
      <h2>props:{{cnum2}}</h2>
      <h2>data:{{dnum2}}</h2>
      <!-- <input type="text" v-model="dnum2"> -->
      <input type="text" :value="dnum2" @input="num2Input">

    </div>
  </template>

  <script>
    const cpn = {
      template: '#cpn',
      props: {
        cnum1: Number,
        cnum2: Number
      },
      data() {
        return {
          dnum1: this.cnum1,		
          dnum2: this.cnum2
        }
      },
      methods: {
        num1Input(event) {
          // 1.将 input 中的value赋值到 dnum中
          this.dnum1 = event.target.value
          // 2.为了让父组件修改值，发出一个事件
          this.$emit('num1change', this.dnum1)
          // 3.修改dnum2的值
          this.dnum2 = this.dnum1 * 100,
          this.$emit('num2change', this.dnum2)
        },
        num2Input(event) {
          this.dnum2 = event.target.value
          this.$emit('num2change', this.dnum2)
          this.dnum1 = this.dnum2/100,
          this.$emit('num1change', this.dnum1)
        }
      }
    }
    const app = new Vue({
      el: '#app',
      data: {
        num1: 1,
        num2: 0
      },
      components: {
        cpn
      },
      methods: {
        num1change(value) {
          this.num1 = parseFloat(value)
          // this.num1 = value
        },
        num2change(value) {
          this.num2 = parseFloat(value)
        }
      }
    })
  </script>
```

演示：![image-20221030181013857](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221030181013857.png) ![image-20221030181032201](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221030181032201.png)



##### 父子组件的访问方式：

有时候我们需要父组件直接访问子组件，子组件直接访问父组件，或者子组件访问根组件

- 父组件访问子组件：使用<font color=red> $children 或 $ref</font>
- 子组件访问父组件：使用 <font color=red>$parent</font>

**父组件访问子组件：$children**

```html
  <div id="app">
    <cpn></cpn>
    <button @click="btnclick">按钮</button>
  </div>
  <template id="cpn">
    <div></div>
  </template>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        message: ''
      },
      components: {
        cpn: {
          template: '#cpn',
          methods: {
            showMessages() {
              console.log('showMessage');
            }
          }
        }
      },
      methods: {
        btnclick() {
          //访问子组件
          console.log(this.$children);
          this.$children[0].showMessages()
        }
      }
    });
  </script>
```

上述中父组件打印并调用了 $children ，输出：![image-20221030204916177](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221030204916177.png)

可知，通过 $children 确实可以访问到子组件的方法或属性

> 通过 $children 访问子组件的属性或方法时得到的是一个数组（[VueComponent]），数组内就是所有的子组件，可以通过 `this.$children[index]`访问每个子组件，但是<font color=skyblue>正是因为是通过下标值访问每个子组件，所以，当组件数量被改变时，就会得到错误的结果，因此这种方式不推荐使用</font>；推荐使用 $refs

**父组件访问子组件：$refs**

$refs 默认是一个空对象，

- 使用 $refs 访问子组件时，如果直接调用 this.$refs 得到的是一个空对象

​	<img src="C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221030210152934.png" alt="image-20221030210152934" style="zoom:80%;" />  输出：![image-20221030210224926](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221030210224926.png)   

- 需要在自定义组件中添加一个 <font color=red>ref </font>属性

​	![image-20221030210506197](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221030210506197.png)<img src="C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221030210152934.png" alt="image-20221030210152934" style="zoom:80%;" />

​	输出：![image-20221030210712450](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221030210712450.png)

**子组件访子组件：$parent**

通过访问子组件的 $parents 拿到的是最近一层的父组件

```html
  <div id="app">
    <cpn></cpn>    
  </div>
  <template id="cpn">
    <div>
    	<button @click="btnclick">按钮</button>
    </div>
  </template>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        message: ''
      },
      components: {
        cpn: {
          template: '#cpn',
          methods: {
             btnclick() {
          		//访问父组件
          		console.log(this.$parent);         		
        	}
          }
        }
      },
      methods: {
       
      }
    });
  </script>
```

输出：![image-20221030211914366](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221030211914366.png)

> 同时在 Vue 实例注册的子组件通过 $root 访问到的也是 Vue 实例



## 组件化高级

### 插槽 slot

#### 为什么使用插槽？

- 插槽的目的是让我们原来的设备具备更多的扩展性

**组件的插槽：**

- 组件的插槽也是让我们封装的组件更具有扩展性
- 让使用者可以决定组件内部的一些内容到底展示什么

#### 如何封装这类组件呢？

![image-20221031105037386](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221031105037386.png)

**比如京东导航栏**

![image-20221031103953182](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221031103953182.png)

![image-20221031104009057](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221031104009057.png)

![image-20221031104104885](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221031104104885.png)

在组件模板中预留一个插槽空间，之后在使用时才决定组件内部要包括什么内容：

 ![image-20221031104610783](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221031104610783.png) ![image-20221031104805384](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221031104805384.png)

打印：![image-20221031104822394](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221031104822394.png)

> 插槽`<slot><button></button></slot>`内部也可以显示一个默认的内容，在使用组件的时候如果自定义组件标点内没有添加内容，就会显示这个默认的内容

#### 具名插槽

- 类似于京东导航栏，有些时候我们展示出来的可能是不同的内容，这时候可以使用具名插槽，来规定要修改的是哪一个

  ![image-20221031104104885](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221031104104885.png)

 ![image-20221031110810230](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221031110810230.png)         <img src="C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221031111241815.png" alt="image-20221031111241815" style="zoom:80%;" />

打印：![image-20221031111217364](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221031111217364.png)

#### 编辑作用域

- 在真正学习插槽之前，需要理解一个概念：**编辑作用域**

- 通过一个例子来理解这个概念：

  ```html
  <div id="app">
      <cpn v-show="isShow"></cpn>
    </div>
  
    <template id="cpn">
      <div>
        <h2>我是标题</h2>
        <p>我是内容</p>
      </div>
    </template>
  
    <script>
      const app = new Vue({
        el: '#app',
        data: {
          message: '',
          isShow: true
        },
        components: {
          cpn: {
            template: '#cpn',
            data() {
              return {
                isShow: false
              }
            }
          }
        },
        methods: {}
      });
  </script>     
  ```

  打印：![image-20221031112334518](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221031112334518.png)

  > 如上述代码：在 app实例内定义一个 isShow变量，在组件中也定义了一个 isShow变量；app 实例模板中使用 v-show动态绑定 isShow，可知绑定的是 app实例的 isShow。所以称 该app模板就是app Vue实例的编辑作用域；同样如果在组件模板中通过 v-show 绑定 isShow ，绑定的就是组件内的isShow 变量，那么就称template标签内的模块就是组件cpn编辑作用域

#### 作用域插槽

核心思想：<font color=red>父组件替换插槽的标签，但是内容由子组件决定</font>

需求：

- 子组件中包括一组数据：pLanguages: ['js','c++','c#','php','java','swift']
- 需要在多个界面进行展示
  - 某些界面是以水平方向进行展示
  - 某些界面是以列表形式展示
  - 某些界面直接展示一个数组
- 内容由子组件决定，父组件告诉我们如何展示，这时候就是用作用域插槽

```html
<div id="app">
    <cpn>
      <template v-slot="slot">		<!--使用v-slot="slot"就可以绑定组件中的slot；访问slot.data就可以访问到pLanguages内的数据-->
        <!-- <span v-for="item in slot.data">{{item}} - </span> -->
        <span>{{slot.data.join(' * ')}}</span>
      </template>
    </cpn>
  </div>

  <template id="cpn">
    <div>
      <slot :data="pLanguages">		<!--动态绑定一个属性，属性内的pLanguages就是组件内data中的pLanguage-->
        <ul>
          <li v-for="item in pLanguages">{{item}}</li>
        </ul>
      </slot>
    </div>
  </template>

  <script>
    const app = new Vue({
      el: '#app',
      data: {
        message: ''
      },
      components: {
        cpn: {
          template: '#cpn',
          data() {
            return{
              pLanguages: ['js','c++','c#','php','java','swift']
            }
          }
        }
      },
      methods: {}
    });
</script>
```

输出：![image-20221031122007360](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221031122007360.png)

> cpn 标签内最好包含一个 template 标签，再输入相关代码
>
> slot 标签绑定的属性可以使用任意属性名



# 4.模块化开发

## CommonJs（了解）

- 模块优有**两个核心**

  - CommonJs的导出：

  ![image-20221031144702314](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221031144702314.png)

  - CommonJs的导入：

    ![image-20221031144916550](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221031144916550.png)

## ES6中的模块化

在代码中引入js模块文件，并且类型需要设置为 module

```js
<script src="info.js" type="module"></script>
```

**export 基本使用**		

> 使用 export 导出的数据，导出的是什么名字，导入时也要使用这个名字

```js
//export 指令用于导出变量
export let name = 'why'
export let age = 18
export let height = 1.88

//上述代码还有另外一种写法：
let name = 'why'
let age = 18
let height = 1.88
export {name, age, height}

//导出函数
export function mul(num1, num2) {
    return num1 + num2
}

//导出类
export class Person() {
    constructor(name, age) {
        this.name = name
        this.age = age
    }
    run() {
        console.log(this.name + '在奔跑')
    }
}
```

别的模块导入：

```js
import {name, age, height} from './a.js'
import {mul, Person} from './a.js'

//使用
console.log(mul(10, 20))
const p = new Person()
p.run()
```

**export default**

某些情况，一个模块中包含某个功能，我们并不希望给这个功能命名，而是希望导入者自己命名，这个时候就使用 export default

> ==一个模块只能有一个 export default==

- 导入导出变量

```js
//a.js导出
const address = '北京'
export default address

//b.js导入
import addr from './a.js'
```

- 导入导出函数

```js
//a.js导出
export default function(argument) {
	console.log(argument)
}

//b.js导入
import fun from './a.js'
fun('你好')
```

**统一全部导入**

```js
//方法一：
import {flag, name, age, Person, mul...} from './a.js'

//方法二：
import * as aa from './a.js'
console.log(aa.flag)
console.log(aa.name)
console.log(aa.age)
...
```



## Webpack

### 1.什么是  webpack

从本质上来讲：<font color=red>webpack 就是一个现代的 JavaScript 应用的静态**模块打包**工具</font>

市面上常见的打包工具：grunk、gulp、rollup、webpack

![image-20221031165936021](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221031165936021.png)

### 2.前端模块化

前端模块化：

- 目前使用前端模块化的一些方案：AMD、CMD、CommonJs、ES6
  - 目前只有 ES6 规范浏览器才支持，其他的规范必须有底层的支撑；而 Webpack 就可作为底层的支撑，可自动将 AMD CMD CommonJs 代码后期做一些转化，转化为浏览器能够识别的代码

 <img src="C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221031170529470.png" alt="image-20221031170529470" style="zoom:80%;" />

 <img src="C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221031170739907.png" alt="image-20221031170739907" style="zoom:80%;" />

### 3.webpack 和 grunt/glup 的对比

![image-20221031170955358](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221031170955358.png)

 <img src="C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221031171021222.png" alt="image-20221031171021222" style="zoom:80%;" />

<img src="C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221031171048899.png" alt="image-20221031171048899" style="zoom:80%;" />

<img src="C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221031171117053.png" alt="image-20221031171117053" style="zoom:80%;" /> 

<img src="C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221031171231653.png" alt="image-20221031171231653" style="zoom:80%;" /> 

### 4. 手动 webpack 的配置

**webpack 为了正常运行，必须依赖 node 环境；而 node 环境为了可以正常地执行更多代码，必须包含各种依赖的包，所以安装了node 环境就自动安装了 npm 工具（ 管理Node 中的各种包的工具）**

![image-20221031172524193](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221031172524193.png)

#### webpack的使用

- ==在项目中，src 一般是开发时的文件夹，dist 一般是发布时候的文件夹；而最终也是将 dist 文件夹打包后发给服务器==

```js
//定义入口函数，导入mathUtils.js和info.js文件

// 使用 CommonJs 规范导入
const { add, mul } = require('./mathUtils.js')

console.log(add(20, 30));
console.log(mul(10, 20));

// 使用 ES6 规范导入
import {name, age, height} from './info'
console.log(name);
console.log(age);
console.log(height);
```

```js
//mathUtils.js
function add(num1, num2) {
  return num1 + num2
}

function mul(num1, num2) {
  return num1 * num2
}

// 使用 CommonJs 规范导出
module.exports = {
  add,
  mul
}
```

```js
//info.js
// 通过 ES6 导出
export const name = 'zs'
export const age = 18
export const height = 20
```

此时如果在需要使用的 html 文件中导入入口文件 main.js 文件是无效的，因为浏览器无法解析 CommonJs，CMD，AMD等的代码，所以需要通过 webpack 打包成浏览器能认识的文件

打包：![image-20221031233533516](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221031233533516.png)

此时在项目目录中就会多一个 dist 文件夹，dist 文件夹内还会包含一个 bundle.js，这个js 文件内包含的就是对 CommonJs等代码进行解析后的代码。最后在需要的 html 文件中引入 bundle.js 就可以在浏览器正常的运行

```js
// index.html 引入bundle.js
<script src="./dist/bundle.js"></script>
```

输出：![image-20221031233844494](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221031233844494.png)

> main.js依赖了 其他的 js 文件，此时不用关心，webpack 会自动解析绑定这些依赖文件

#### webpack配置：webpack.config.js

有的时候我们不想在终端指定对应的要打包的文件以及打包到的哪个目录文件文件

- 可在项目根目录中创建一个 webpack.config.js 文件，一旦确定了要打包的文件和目的地址，webpack就会自动读取。

  ```js
  //导入 path 模块
  const path = require('path')
  
  //通过CommonJs指定要导出的内容
  module.exports = {
  	entry: './src/main.js',								//指定对应的入口文件
  	output: {											//指定对应的出口文件
          path: path.resolve(__dirname, 'dist'),      	//动态添加路径(绝对路径)
          filename: 'bundle.js'
      }		
  }
  ```

- 直接在终端输入 webpack 即可完成打包

  ![image-20221101140903963](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221101140903963.png)

- 此外，输入 `webpack `在后期可能会加入很长的后缀，所以可以使用 `npm run build`与之映射

  - 在 package.json 文件找到 "script"属性，添加=="built": "webpack"== 就可以完成 webpack 与 `npm run build`的映射。![image-20221101141416060](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221101141416060.png)

- 这个时候在终端输入 `npm run build`就可实现打包

   <img src="C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221101141620766.png" alt="image-20221101141620766" style="zoom:80%;" /> 成功将入口文件打包至bundle.js![image-20221101141736591](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221101141736591.png)

#### 局部安装 webpack

目前，使用的 webpack 是全局的 webpack 

- 因为一个一个项目往往依赖特定的 webpack 版本，全局的版本可能和这个项目的webpack 版本不一致，导致打包出问题
- 所以通常一个项目都有自己局部的 webpack

通过命令`npm install webpack@3.6.0 --save-dev`将 webpack 的3.6.0版本安装为开发时才依赖的包

- 敲了这个命令后，编辑器就会寻找本地的 node_module/.bin 路径中对应的命令，如果没有找到就会在全局的环境变量中寻找
- 执行：`npm run build`	

> 补充：所有在终端或者 cmd 敲的命令，都是在全局中进行查找；而一旦在package.json 的 'script'属性内定义了对应的脚本，就会优先使用本地的包![image-20221101141416060](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221101141416060.png)

### 5.loader

**loader 是webpack 中一个非常核心的概念**

![image-20221101144006899](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221101144006899.png)

loader 使用过程：

- 步骤一：npm 安装 loader
- 步骤二：在 webpack.config.js 中的 modules 关键字下进行配置

#### webpack-css文件的处理

定义一个normal.css文件：![image-20221101154057247](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221101154057247.png)![image-20221101154108334](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221101154108334.png)

- 在模块化中，对于我们的 css 文件，我们在引用时一般是在入口文件直接导入这些 css 文件，而不是使用 link 标签在 html 文件中引入

  ```js
  //main.js
  
  // 依赖 css 文件
  require('./css/normal.css')
  ```

- 导入 css文件后，安装 style-loader 和 css-loader（注意版本）

  `npm install -save -dev style-loader@0.23.1`

  `npm install -save -dev css-loader@2.0.2`

- webpack.config.js 文件中配置 style-loader 和 css-loader

  ```js
  module.exports = {
    module: {
      rules: [{
        test: /\.css$/,
        use: ['style-loader', 'css-loader']
        //css-loader 只负责将 css 文件进行加载
        //style-loader 负责将样式添加到 DOM 中
        //使用多个 loader 时，从右往左
      }]
    }
  }
  ```

  > 注意：属性use中的 style-loader 和 css-loader 顺序不能调换，因为 webpack 在读取时是从又往左

- `npm run build`打包

运行 index.html 文件，效果：![image-20221101154033263](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221101154033263.png)

#### webpack-less文件的处理

定义一个 special.less 文件![image-20221101160913362](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221101160913362.png) 内容：![image-20221101160926351](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221101160926351.png)

- 在main.js 文件中依赖 less 文件

  ```js
  //main.js
  
  // 依赖 less 文件
  require('./css/special.less')
  ```

- 安装 less-loader （开发时依赖）

  `npm install --save-dev less-loader@4.1.0 less`

  > 注意：less-loader 要注意版本限制；并且 less-loader 还要依赖 less ，所以 less 也要安装

  ![image-20221101162500900](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221101162500900.png)

- webpack.config.js 文件中配置 less-loader

  ```js
  module.exports = {
    module: {
      rules: [{
        test: /\.less$/,
        use: [{
          loader: "style-loader" // creates style nodes from JS strings
        }, {
          loader: "css-loader" // translates CSS into CommonJS
        }, {
          loader: "less-loader" // compiles Less to CSS
        }]
      }]
    }
  }
  ```

- `npm run build`打包

效果：![image-20221101162708217](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221101162708217.png)

#### webpack 图片资源的处理

- 先在目录中创建 img 文件夹，准备两张==大小不一（一张为24.5kb，一张为30.1kb）==的图片

![image-20221101170612180](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221101170612180.png)

- ==先在 normal.css 文件内引入其中一张较小的图片==

  ![image-20221101170820544](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221101170820544.png)

  - 安装 url-loader

    `npm install --save-dev url-loader@0.6.2`

    > 注意：如果版本过高，图片地址会显示   background: url([object Object])

  - webpack.config.js 文件中配置 url-loade

    ```js
    module.exports = {
      module: {
        rules: [{
          test: /\.(png|jpg|gif|jpeg)$/,
          use: [{
            loader: 'url-loader',
            options: {
              // 当加载的图片小于 limit 时，会将图片解析成 base64 格式的字符串
              // 当加载的图片大于 limit 时，需要使用 file-loader模块 进行加载
              limit: 28000			//limit 默认为8192
            }
          }]
        }]
      }
    }
    ```

  - `npm run build`打包，之后会发现，浏览器将图片的 url 地址解析成了<font color=red> base64 位</font>的字符串

- ==在 normal.css 文件内引入其中一张较大的图片==

  - 如果图片的大小大于了 limit 的限制，那么需要使用 file-loader模块 进行加载

    `npm i file-loader@4.2.0 --save-dev `

  - 再次打包就会发现 dist 文件夹里面多了一个图片文件

    ![image-20221101210355283](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221101210355283.png)

  - 我们会发现 webpack 自动帮我们把这个图片文件生成了一个非常长的名字

    - 这是一个32位的 hash 值，目的是防止名字重复
    - 但是真实开发中我们可能对打包的图片名字有一定的要求

  - 所以我们可以在 option 中添加如下选项

    ![image-20221101213444377](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221101213444377.png)

  - 但是图片仍然没有显示出来，这时因为图片路径不正确

    - 默认情况下：webpack 会将生成的路径直接返回给使用者

    - 但是，整个程序是打包在 dist 文件夹下的，所以需要在路径下添加 dist/

      ![image-20221101211340079](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221101211340079.png)

  - 打包后会发现dist 文件夹下多一个 img 文件加，img 文件夹下就有这个修改名字后的图片

    ![image-20221101213601921](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221101213601921.png)

#### ES6 语法处理

如果仔细阅读 webpack 打包的 js 文件，会发现写的 ES6 语法并没有转化成 ES5，所以有些浏览器可能不能识别

所以可以使用 babel 这个工具

- 而在 webpack 中，直接使用 babel 对应的 loader 就可以

  <font color=red>`npm install babel-loader@7 babel-core babel-preset-es2015 --save-dev`</font>

- 配置 webpack.config.js 文件

  ```js
  module.exports = {
      module: {
        rules: [
          {
            test: /\.js$/,
            exclude: /(node_modules|bower_components)/,
            use: {
              loader: 'babel-loader',
              options: {
                presets: ['es2015']
              }
            }
          }
        ]
      }
  }    
  ```

- 重新打包，就会发现 bundle.js 中的代码转为了 ES5 的语法

  ![image-20221101220648423](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221101220648423.png)

#### 引入 Vue.js

- 首先安装 Vue

  ` npm i vue@2.5.21 -s`

- 在入口文件中导入 Vue 模块，并在 index.html 文件中使用

  ```js
  //main/js
  // 使用 Vue 进行开发
  import Vue from 'vue'
  
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好'
    }
  })
  ```

  ```html
  <!--index.html-->
  <div id="app">
  	<h2>{{message}}</h2>
  </div>
  ```

  

- 但是，这个时候由于 Vue发布的时候有两类版本，他们其中的一类不会解析 template模板的代码，所以要在 webpack.config.js 中对 Vue 进行配置

  ```js
  module.exports = {
     resolve: {
      alias: {
        'vue$': 'vue/dist/vue.esm.js'
      }
    }
  }
  ```

  > 这一段代码的意思是，当使用 import 导入 Vue 模块的时候，会去 node_modules 找指定的 vue/dist/vue.esm.js文件，并读取这里面的代码，这个时候就可以解析 template 有关的代码

- 重新打包

  ![image-20221101223418620](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221101223418620.png)

##### template 与 el 的关系

我们在自定义了组件后，不希望频繁修改 index.html ，这个时候就可以使用 ==template 属性==

定义 template 属性：

![image-20221102103047669](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221102103047669.png)

main.js 文件中：![image-20221102104608255](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221102104608255.png)

index.html 文件中：![image-20221102105141546](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221102105141546.png)

> 上述这种方式中，Vue内部会自动将 index.html 文件的 app模板替换为 template 内的 html 代码

##### Vue 中template 的升级写法

**升级写法一：**

将 Vue实例中 template 、data、methods内的代码抽离成一个 App 组件，而在 Vue 实例中只需注册这个 App 组件，并在 template 内使用这个组件即可

```js
//main.js

import Vue from 'vue'

const App = {
  template: `
    <div>
      <div>{{message}}</div> 
      <p>我是草泥马</p>
      <button @click="btnclick">按钮</button>
    </div>
  `,
  data() {
    return {
        message: '你好',
      }
  },
  methods: {
    btnclick() {
      alert('李银河')
    }
  }
}

new Vue({
  el: '#app',
  template: '<App/>',	//将index.html文件中app模板替换为了<App/>组件
  components: {
    App
  }
})
```

**升级写法二：**

抽离出的App组件相关的内容同样可以封装到一个 Vue 文件夹中：

- 新建一个 Vue文件夹， Vue文件夹下新建一个 app.js 文件

  ```js
  //app.js
  
  export default {
    template: `
      <div>
        <div>{{message}}</div> 
        <p>我是草泥马</p>
        <button @click="btnclick">按钮</button>
      </div>
    `,
    data() {
      return {
        message: '你好',
      }
    },
    methods: {
      btnclick() {
        alert('李银河')
      }
    }
  }
  ```

- main.js 引入 app.js 文件

  ```js
  //main.js
  
  // 导入 app.js 文件
  import App from '../../vue/app'
  
  new Vue({
    el: '#app',
    template: '<App/>',
    components: {
      App
    }
  })
  ```

##### Vue 中 template 的最终写法

前面升级写法二中还有一个问题就是：**模板和 js 代码没有分离，所以这种写法也要舍弃**

所以可以用下面这种最终写法：在 vue 文件夹下新建一个 app.vue 文件，将模板和js代码以及样式进行抽离，如下代码：

```vue
<template>
  <div>
    <div>{{message}}</div> 
      <p>我是草泥马</p>
      <button @click="btnclick">按钮</button>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      message: '你好',
    };
  },
  methods: {
    btnclick() {
      alert('李银河')
    }
  }
}
</script>

<style scoped>

</style>
```

 而最后，只要在 main.js 中引入 app.vue 文件即可

```js
//main.js

// 导入 app.vue 文件
import App from './vue/app.vue'
```

但是，现在还无法使用 `npm run build` 进行打包，因为 webpack不能识别 vue 代码，所以要对 .vue 文件进行封装处理。

##### .vue 文件封装处理

- 安装 vue-loader 和 vue-template-complier

  `npm i vue-loader@13.0.0  --save-dev ` 

  `npm i vue-template-complier@2.5.21 --save-dev`	

  > 注意：
  >
  > vue-template-complier 版本号需要跟 vue 保持一致

- 配置 webpack.config.js

  ```js
  module.exports = {
      module: {
        rules: [
          {
            test: /\.vue$/,
            use: ['vue-loader']
          }
        ]
      }
  }    
  ```

  > 如果 vue-loader 版本在15以上就要配置一个插件
  >
  > ```js
  > //webpack.js
  > 
  > //两个方式都可以的，随便用一个
  > const VueLoaderPlugin = require('vue-loader/lib/plugin');
  > 
  > // 或者 
  > const { VueLoaderPlugin } = require('vue-loader')
  > plugins: [
  >     // make sure to include the plugin for the magic
  >     new VueLoaderPlugin()
  > ]
  > ```

打印：![image-20221102114510917](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221102114510917.png)

##### 尝试在 App.vue 组件中在注册一个 Cpn.vue 组件

- 在 vue文件夹下新建一个 Cpn.vue 文件

![image-20221102115324775](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221102115324775.png)

- Cpn.vue 定义内容

  ```vue
  <template>
    <div>
      <div>{{message}}</div>
      <h2>{{doc}}</h2>
    </div>
  </template>
  
  <script>
  export default {
    name: 'Cpn',
    data () {
      return {
        message: '我是Cpn组件',
        doc: '哈哈哈哈'
      };
    },
    methods: {}
  }
  </script>
  
  <style scoped>
  
  </style>
  ```

- 在 App.vue 文件中引入、注册并使用 Cpn.vue 组件

  ![image-20221102115606056](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221102115635741.png)![image-20221102115656655](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221102115656655.png)![image-20221102115618625](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221102115618625.png)

### plugin

loader 和 plugin 的区别：

- loader 主要用于转换某些类型的模块，它是一个转换器
- plugin 是插件，它是对 webpack 本身的扩展，是一个扩展器

plugin的使用过程：

- 步骤一：通过 npm 安装需要使用的 plugin （某些 webpack 已经内置的 plugin 不需要安装）
- 步骤二：在 webpack.config.js 中的 plugins 中配置插件

##### 1.添加版权的plugin

<font color=red>BannerPlugin插件</font>：属于webpack 自带的插件，可以为打包的文件添加版权声明

操作如下：

- 因为是 webpack 自带的插件，所以直接导入 webpack 模块就行，不用 npm 安装插件

- 修改 webpack.config.js 文件的配置

  ![image-20221103135948295](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221103135948295.png)

- 之后再重新打包程序：查看 bundle.js 文件的头部，看下如下信息：

  ![image-20221103140042245](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221103140042245.png)

##### 2.处理 html 文件的插件

之前我们的 index.html 文件都是放在根目录下的，但是我们打包后上线的文件夹是dist文件夹，并且我们的 index.html 我们也要一并打包进去，所以这个时候可以使用一个插件：<font color=red>HtmlWebpackPlugin 插件</font>将我们的index.html文件一起打包到 dist 文件夹下

安装了 HtmlWebpackPlugin 插件可以为我们做的事：

- 自动生成一个 index.html 文件（可以指定模板来生成）
- 将打包的 js 文件，自动通过 script 标签插入到 body 中

使用步骤：

- 安装插件（注意版本）

  `npm i html-webpack-plugin@3.2.0 --save-dev`

- 修改 webpack.config.js 文件夹下 plugins 内的相关参数

  ```js
  //导入 html-webpack-plugin 插件
  const HtmlWebpackPlugin = require('html-webpack-plugin') 
  
  
  module.exports = {
      plugins: [                  //配置对应插件
        new webpack.BannerPlugin('最终版权归DuMer所有'),
      new HtmlWebpackPlugin({
        template: 'index.html'		
      })
    ]
  }
  ```

- 这个时候再次打包程序，就会自动去 webpack.config.js 文件的当前目录中找到 index.html 文件，并复制一份打包到 dist 文件夹下

  ![image-20221103144309129](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221103144309129.png)

> 注意：为了使打包的 index.html 文件能够成功导入 bundle.js ，并且包含 app模块，要先删除原先index.html 文件内的导入 bundle.js 的代码，并且删除 webpack.config.js 内output内的 publicPath代码![image-20221101211340079](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221101211340079.png)

##### 3. js 压缩的plugin

对 js 文件进行压缩，可以使用 <font color=red>uglifyjs-webpack-plugin 插件</font>，并且版本指定1.1.1，和 CLI2 保持一致

使用步骤：

- 安装 uglifyjs-webpack-plugin 插件

  `npm install uglifyjs-webpack-plugin@1.1.1 --save-dev`

- 修改webpack.config.js 文件，使用插件：

  ![image-20221104120702707](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221104120702707.png)

- 重新打包，就可发现 bundle.js 已经被压缩

  <img src="C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221104121113886.png" alt="image-20221104121113886" style="zoom:80%;" />

  > 注意：如果是在开发阶段，不建议使用丑化js代码的插件，因为不方便调试

### 搭建本地服务器

- webpack 提供了一个可选的本地开发服务器，这个本地服务器基于node.js搭建，内部使用 express 框架，可以实现我们想要的让浏览器自动刷新显示我们修改后的结果

- 使用 webpack-dev-server 搭建一个本地服务器

- devserver也是作为 webpack 中的一个选项，选项本身可以设置如下属性：
  - contentBase：表示为哪一个文件夹提供本地服务，默认是跟文件夹，外面这里可以填写./dist
  - port：端口号
  - inline：页面实时刷新
  - historyApiFallback：在 SPA 页面中，依赖 H5 的 history 模式

**使用步骤：**

- 它是一个单独的模块，使用前要先安装

  `npm i webpack-dev-server@2.9.1 --save-dev`

- webpack.config.js 的配置如下

  ```js
  module.exports = {
   devServer: {              //搭建本地服务器
      contentBase: './dist',
      inline: true
    }
  }
  ```

- 在package.json 文件中配置脚本 ![image-20221104171421341](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221104171421341.png)

- 之后在终端输入`npm run dev`即可运行

> 如果在脚本 `webpack-dev-server`后面加上 --open ，再使用`npm run dev`运行就会自动打开网页

### webpack 配置文件进行分离

- 根据开发时和发布时的情况对配置文件进行抽离；开发时使用是个配置文件，而在发布时使用另一个配置文件



## Vue CLI 相关

### 1.Vue CLI是什么？

- 如果在开发大型项目，那么就必须要使用  Vue CLI
  - 使用 Vue.js 开发大型项目时，我们需要考虑代码目录结构、项目结构和部署、热加载、代码单元测试等事情
  - 如果每个项目都要手动完成这些事情，那么效率就会非常低，所以通常会使用脚手架工具来帮助完成
- CLI 是什么意思？
  - CLI 是 Command-Line Interface ，翻译为命令行界面，但是俗称脚手架
  - Vue CLI 是一个官方发布的 Vue.js 项目脚手架
  - 使用 Vue-cli 可以快速搭建 Vue开发环境以及对应的 webpack 配置

#### 1.1 Vue CLI 使用前提 - Node

```shell
//安装淘宝镜像
npm i -g npm --registry=https://registry.npm.taobao.org

//安装完后就可以使用 
cnpm install ...
```

#### 1.2 Vue CLI 使用前提 - webpack

<img src="C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221104174653444.png" alt="image-20221104174653444" style="zoom:80%;" /> 

#### 1.3 Vue CLI的使用

- **安装 Vue 脚手架（已出5版本）**

  `npm i @vue/cli -g`

  > 这个命令安装的 Vue CLI 3，使用如下命令就可以即使用版本2的模板，又可以使用版本2的模板
  >
  > `npm i @vue/cli-init`

##### **1.3.1 使用VueCLI2创建项目**

`vue init webpack my-project`

使用脚手架2创建项目前会有如下参数

![image-20221104183721262](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221104183721262.png)

​		**目录结构详解：**

​		![image-20221104200301545](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221104200301545.png)

**关于使用 Vue CLI2创建项目时选择的两个参数：<font color=red>runtimecompiler</font> 和 <font color=red>runtimeonly</font>**

- 选择 runtimecompiler 的项目和选择 runtimeonly 的项目==区别==就是在入口文件 main.js ，如下图：

  ![image-20221104212543481](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221104212543481.png)
  
  - 根据创建项目时，所选的类型有这样一段话：![image-20221105205008592](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221105205008592.png)
  
    > 上述带代码说的是使用的  Runtime-only 创建的项目会比使用 Runtime-Compiler 小6kb，原因就是：Vue 在解析 Vue实例代码的时候会经过以下过程：
    >
    > ```
    > template ——> ast ——> render函数 ——> virtual ——> UI
    > ```
    >
    > 上述过程其实就是 Runtime-Compiler 的运行过程，而<font color=red>使用 Runtime-only 创建的项目直接跳过了 template——>ast的步骤，所以会比前者要小6kb，所以 Runtime-only 方式代码量少，性能更高</font>
    >
    > 
    >
    > 而导入的 Vue 文件内虽然也有 tempalte 模板如图：![image-20221105215310767](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221105215310767.png)
    >
    > 但是，Vue 内部的 Vue-tempalte-compiler![image-20221105215559651](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221105215559651.png)  已经将这个 template 模板转化为了render 函数了，所以仍然不需要经过`template ——> ast ——> render函数`这个步骤
    >
    > 

**关于 Vue 实例中的 render 函数**	

根据上节内容可知，使用 Runtime-only 创建的项目，它的 main.js 中是使用 render函数渲染节点的，具体实现原理如下：

```js
new Vue({
  el: '#app',
  // 原理：
  render: function(createElement) {
    //render函数内其实是传入了一个createElement，这个createElement可以创建一个节点
    // createElement传入了三个参数，分别是：标签名（字串格式）、标签属性（对象类型）、内容（数组类型）
    // 1.普通用法  
    return createElement('h2', {class: 'box'}, ['hello world'])
  }
})
```

- 一旦确定了createElement 创建的节点，就会自动添加到 index.html 文件，并进行渲染，如下图：

  ![image-20221105211904542](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221105211904542.png)

```js
const cpn = {
    template: '<div>{{message}}</div>',
    data() {
        return {
            message: '我是组件的message'
        }
    }
}

new Vue({
  el: '#app',
  render: function(createElement) {
    //2.传入一个组件对象
  	return createElement(cpn)
  }
})
```

打印（这种写法只适合Runtime-compiler）：![image-20221105213710301](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221105213710301.png)

上述代码可知，createElement 内可以传入一个组件，这正是使用 Runtiem-only 创建的项目的 main.js 中的 render函数渲染节点的解析

```js
//Runtime-compiler
const cpn = {
  template: '<div>{{message}}</div>',
  data() {
    return {
      message: '我是组件的message'
    }
  }
}
new Vue({
  el: '#app',
  render: function (createElement) {
    //2.传入一个组件对象
    return createElement(cpn)
  }
})

//Runtime-only
import App from './App'
new Vue({
  el: '#app',
  render: function(h) {
    return h(App) 
  }
})

```

**关于 `npm run build`**

![image-20221105220003484](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221105220003484.png)

关于  `npm run dev`

![image-20221105220107569](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221105220107569.png)



##### **1.3.2 使用 Vue CLI3 创建项目（CLI5 也适用下面的命令）**

`vue create my-project`

- 创建完项目后，目录结构如图。红色框内就是使用创建项目命令生成的项目文件夹，绿色框内的就是创建脚手架时就产生的文件夹

![image-20221104182650995](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221104182650995.png)

- 打开项目后，如下图所示结构：

  ![image-20221104182835596](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221104182835596.png)
  
  > package-loack.json：里面都是些 node 包具体的版本信息，而 package.json 里面的就是些大概的版本

### 2.Vue CLI3 的使用

Vue CLI3 与 2 的版本的区别：

<img src="C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221105220752281.png" alt="image-20221105220752281" style="zoom:80%;" />

- 查看一下项目目录（这个真实的版本为CLI5的版本，但是跟CLI3差不多）：![image-20221104182835596](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221104182835596.png)

> public文件夹内的内容在项目打包是也会原封不动地打包到 dist 文件夹内

- 打开 /src/main.js 文件，如下图：注意这里有个东西要设置为 false，目的是防止在`npm run build`后关闭一些提示信息![image-20221105223724850](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221105223724850.png)查看使用 CLI3创建的项目的main.js 和CLI2创建的项目的main.js，进行比较![image-20221105224110596](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221105224110596.png)![image-20221105224024209](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221105224024209.png)

  仔细查看绑定app的方式不一样，其实以前使用 el 绑定元素的方式实际上也是通过 .$mount()实现的

#### 开启本地服务创建 Vue 项目

在任意终端输入命令`vue ui`即可开启本地服务

![image-20221106105842755](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221106105842755.png)

在网页中会自动打开用户界面：

![image-20221106105908538](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221106105908538.png)

在这个图形化界面中可创建Vue项目，也可以查看和修改相关的配置

### 3.箭头函数补充

**关于箭头函数中的this问题：**

```js
setTimeout(function() {
  console.log(this);         //--window
},1000)

setTimeout(() => {
   console.log(this);        //--window
},1000)
```

```js
const obj = {
  aaa() {
    setTimeout(function() {
      console.log(this);				//--window
    },1000),
    setTimeout(() => {
      console.log(this);                //--{aaa.fn{...}}
    },1000)
  },      
}

obj.aaa()
```

**疑问：为什么setTimeout中的函数this指向window？而箭头函数this指向Object ？**

**解释：**setTimeout()调用的代码运行在与所在函数完全分离的执行环境上，可以认为 setTimeout 就是 window自身的一个方法，所以setTimeout()中的函数始终指向window，但是<font color=red>setTimeout() 中的箭头函数不一样，在箭头函数中的this，总是指向词法作用域，简单地说就是向外层作用域中，一层层查找this，直到有this的定义，如果箭头函数所在的setTimeout写在全局中，那么this指向的就是 window，如果写在函数内部，那么this指向的就是这个函数。</font>

练习：

```js
const obj = {
  aaa() {
    setTimeout(function () {
      setTimeout(function () {
        console.log(this)			//--window
      })

      setTimeout(() => {
        console.log(this);			//--window
      })
    })

    setTimeout(() => {
      setTimeout(function () {
        console.log(this);			//--window
      })
      setTimeout(() => {
        console.log(this);			//--{aaa.fn{...}}
      })
    })
  }
}

obj.aaa()
```

​	

# 5.Vue-router

## 5.1 认识路由

路由中有一个非常重要的概念叫路由表

- 路由表本质就是一个映射表，决定了数据包的指向

路由中提供了两种机制

- 路由是决定数据包从==来源==到==目的地==的路径
- 转送将==输入端==的数据转移到合适的==输出端==

### 关于网页渲染的三种方式：

- 后端渲染阶段：![image-20221106154533880](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221106154533880.png)

- 前后端分离阶段：![image-20221106154628206](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221106154628206.png)

- 单页面富应用阶段（前端路由阶段）：![image-20221106155648004](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221106155648004.png)

前端路由的核心：<font color=red>改变 URL，页面整体不刷新</font>



### URL 的 hash 和 HTML5 的 history

关于前端路由的核心，也就是改变 URL，页面整体不刷新，那么可以怎么实现呢？

这里有两种方式：

**1.URL的hash**

- URL 的 hash也就是锚点（#），本质是改变 window.location 的 href 属性
- 我们可以通过直接赋值 location.hash 来改变 hash，但是页面不发生刷新（没有向服务器发送请求）

![image-20221108114639114](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221108114639114.png)

![image-20221108113656067](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221108113656067.png)

**2.HTML5中的 history**：  **pushState**

通过修改 HTML5中 history的 pushState 属性也可改变 URL，但是页面不刷新

![image-20221108114740031](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221108114740031.png)

> <font color=red>以上两种方式location.hash、history.pushState()来改变 URL 地址的方式都类似于数据结构的出栈和入栈，遵循的先入后出的原则，也就是说每次使用这些方法改变一个 url，那么地址栏中永远都是显示的最后的这个地址，同时可以使用 history.back() 方法对网页进行回退(清除栈顶)，类似于网页左上角的回退按钮。</font>

**3.HTML5中的 history模式：replaceState**

history 中的 <font color=red>replaceState() 方法</font>与 pushState() 相比较的区别就是前者<font color=blue>无法回退</font>。

**4.HTML5中的 history模式：go**

history模式中的 go() 方法类似于 history.back()，都可以对网页进行回退，但是 history.go() 可以传入参数，指定要回退的具体层数；如 history.go(-1) 就等同于 history.back()，也就是回退一层。history.go(2)表示前进两层

**5.HTML5中的 history模式：forward**

history.forward() 等同于 history.go(1)，也就是网页前进的效果



## 5.2 认识 vue-router

目前前端流行的三大框架，都有自己的路由实现：

- Angular 中的 ngRouter
- React 中的 ReactRouter
- Vue 中的 vue-router

vue-router 是基于路由和组件的

- 路由用于设定访问机制，将路径和组件映射起来
- 在 vue-router 的单页面应用中，页面路径的改变就是组件的切换

### 安装和使用 vue-router

通过 webpack，后续开发中我们就可以使用工程化的方式进行开发

步骤一：安装 vue-router（注意版本）

- npm i vue-router@3..0.1 --save

步骤二：在模块化工程中使用（因为是一个插件所以可以通过 Vue.use() 来安装路由功能）

- 第一步：<font color=red>导入</font>路由对象，并且<font color=red>调用 Vue.use(VueRouter)</font>

- 第二步：创建<font color=red>路由实例</font>，并且传入路由<font color=red>映射配置</font>
- 第三步：在<font color=red> Vue实例中挂载创建的路由实例</font>

```js
// router/index.js

// 配置路由相关信息
import VueRouter from 'vue-router'
import Vue from 'vue'

// 1.通过 Vue.use(插件) 安装插件（只要是插件就要使用这一步）
Vue.use(VueRouter)

const routes = [
  // 配置路由和组件的映射关系(一个映射关系就使用一个对象)
]

// 2.创建 VueRouter 对象
const router = new VueRouter({  
  routes
})

// 3.将 router 对象传入 vue 实例中
export default router
```

```js
//main.js

import router from './router'

new Vue({
  router: router,
  render: h => h(App),
}).$mount('#app')

```

使用 vue-router 的步骤

- 第一步：创建路由组件

  ![image-20221108200159625](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221108200159625.png)	![image-20221108200234566](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221108200234566.png)

- 第二步：配置路由映射：组件和路径映射关系

  ![image-20221108200459702](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221108200459702.png)

- 第三步：使用路由：通过 ` <router-link>` 和 ` <router-view> `

  ![image-20221108200621416](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221108200621416.png)

  效果：

  ![image-20221108200739581](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221108200739581.png) ![image-20221108200758792](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221108200758792.png)

  > `router-link`：该标签是 vue-router 已经内置的组件，它会被渲染成一个a标签
  >
  > `router-view`就表示一个占位标签，添加在`view-router`前面，则组件的内容就显示在前面。反之就显示在后面。该标签会根据地址栏的当前路径，显示对应组件的内容
  >
  > 在路由前换时，切换的是 `<router-view>`  挂载的组件，其他内容不会发生改变

#### 设置默认路径

默认情况下，我们希望进入网站的首页，`<rouer-view>` 就显示首页的内容

解决方式：只需要多配置一个映射即可

![image-20221108202131558](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221108202131558.png)

配置解析：

- path 配置的是跟路径 ：/
- redirect 是重定向，也就是我们将根路径重定向到 /home 的路径下

效果：![image-20221108202415013](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221108202415013.png)

#### 使用 history 模式显示路径

我们前面默认修改的都是 hash 值改变 url，我们会发现路径会多一个 #，不美观

这个时候我们可以使用 HTML5中的 history 模式修改路径

操作如下：

- 在 /router/index.js 文件中的创建路由对象过程中加一个 `mode: 'history'`即可

  ![image-20221108203135281](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221108203135281.png)

效果：如下图，# 符号消失

![image-20221108203224482](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221108203224482.png)

#### `router-link`补充

- 在前面的`<router-link>`中，我们只是使用了一个<font color=red>属性：to</font>，用于指定跳转的路径

- `<router-liink>`还有一些其他属性：

  - <font color=red>tag</font>：tag可以指定`<router-link>`之后渲染成什么组件，比如下面的代码会被渲染成一个 <li> 标签，而不是 <a> 标

    ```vue
    <router-link tag="li" to="/home"></router-link>
    ```

  - <font color=red>replace</font>：这个属性没有值，replace 不会留下 history 记录，所以指定了 replace 的情况下，后退键返回不能返回到上一个页面

  - <font color=red>active-class</font>：当 `<router-link>` 对应的路由匹配成功时,会自动给当前元素设置一个 router-link-active 的 class，设置 active-class 可以修改默认的名称

    - 在进行高亮显示的导航菜单或者底部 tabbar 时，会使用到该类
    - 但是通常不会修改类的属性，会直接使用默认的 `router-link-active`

    **具体说明**：当我们的 `router-link` 处于活跃状态时（比如它是一个button，被点击的状态），它会自动添加一个类，如下图

    ![image-20221108224148225](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221108224148225.png)

    这个`router-link-active`类可以满足一些特定的需求，比如当前处于活跃 `router-link` 处于活跃状态时，把它的字体变成红色等，直接在 css 模块中修改即可，如：

    ![image-20221108224918701](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221108224918701.png)效果：![image-20221108224937977](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221108224937977.png)

    同时，我们也可以手动修改 `router-link-active`这个类的名字，直接在 `router-link`内添加一个属性

    `active-class`，并修改为想要使用的名字即可。如：

    ```vue
    <router-link to="/home" tag="button" active-class="active">首页</router-link>
    ```

    ![image-20221108225554040](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221108225554040.png)      效果：![image-20221108224937977](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221108224937977.png)

    > 因为这个只能在`router-link`标签内部手动修改，如果有多个组件的话很麻烦，所以可以使用另一种方法进行<font color=red>统一地修改这个 router-link-active 类</font>。就是直接在路由的配置文件 index.js 中修改，操作如下：
    >
    > ![image-20221108230059381](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221108230059381.png)

#### 通过手动编写代码改变路径		

前面说的都是通过给`router-link`添加 to 属性跳转路由，同时我们也可以手动修改代码进行这个操作，具体操作如下：

- 首先要先明白一点：<font color=blue>每个组件内都有一个 Vue 定义过的一个属性，叫 <font color=red>**$router**</font> 属性</font>				

- 只需通过修改 组件的 $router.push() 即可实现跳转

  ```vue
  <template>
    <div id="app">
      <button @click="homeClick">首页</button>
      <button @click="aboutClick">关于</button>
      <router-view></router-view>
    </div>
  </template>
  
  <script>
  
  export default {
    name: 'App',
    methods: {
      homeClick() {
        // 通过代码的方式修改路由，this指向的是当前组件
        this.$router.push('/home')
      },
      aboutClick(){
        this.$router.push('/about')
      }
    }
  }
  </script>
  ```

效果：

![image-20221108233638391](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221108233638391.png) 点击关于按钮：![image-20221108233652240](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221108233652240.png)

> 这里加入我们不想要跳转之后可以回退到上一级页面的话，就可以使用 `$router.replace()` 替代 `$router.push()`，这样跳转之后的页面就不会回退到上一级页面

#### 动态路由(路径携带参数)

- 在某些情况下，一个页面的 path 路径可能是不确定的，比如我们进入用户界面时，希望是如下的路径：
  - /user/aaa 或 /user/bbb
  - 也就是除了前面的 /user 之外，后面还跟了用户的 ID
  - 这种 path 和 Component 的匹配关系，我们称之为动态路由（也是路由传递数据的一种方式）

- 具体操作如下：

  ![image-20221109114806258](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221109114806258.png)

  ![image-20221109114859811](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221109114859811.png)

  ![image-20221109114842883](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221109114842883.png)

  这样就可以在路径后得到传入的 id

  ![image-20221109114954783](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221109114954783.png)

- 假如想在用户组件内拿到这个 id ，可使用下面这种方式：

  - 在 User 组件中

  ![image-20221109115148656](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221109115148656.png)

  ![image-20221109115201714](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221109115201714.png)

  - 效果：                       ![image-20221109115301086](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221109115301086.png)

  - 或者使用简便写法：![image-20221109115422893](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221109115422893.png)

  - 效果：                      ![image-20221109115301086](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221109115301086.png)

> $router 和 $route 的区别：
>
> 1、$router 是用来操作路由，$route 是用来获取路由信息
>
> 2、$router是 VueRouter 的一个实例，他包含了所有的路由，包括路由的跳转方法，钩子函数等，也包含一些子对象（例如history）
>
> 3、$route 是一个跳转的路由对象（路由信息对象），每一个路由都会有一个$route对象，是一个局部的对象。
>
> - $router 的用法：
>
>   ```js
>   //常规方法
>   this.$router.push("/login");
>   //使用对象的形式 不带参数
>   this.$router.push({ path:"/login" });
>   //使用对象的形式，参数为地址栏上的参数
>   this.$router.push({ path:"/login",query:{username:"jack"} }); 
>   使用对象的形式 ，参数为params 不会显示在地址栏
>   this.$router.push({ name:'user' , params: {id:123} });
>   ```
>
> - $route 的用法：
>
>   ```js
>   主要的属性有：
>   this.$route.path 字符串，等于当前路由对象的路径，会被解析为绝对路径，如/home/ews
>   this.$route.params 对象，包含路由中的动态片段和全匹配片段的键值对，不会拼接到路由的url后面 
>   this.$route.query 对象，包含路由中查询参数的键值对。会拼接到路由url后面
>   this.$route.router 路由规则所属的路由器
>   this.$route.name 当前路由的名字，如果没有使用具体路径，则名字为空
>   ```

#### 路由懒加载

一般情况下，我们的 vue 项目进行打包后的 js 文件夹中会生成<font color=blue> 3个 js 文件 </font>

- app.xxx.js：程序员写的业务代码
- manifest.xxx.js：为 ES6、Commonjs 做底层支撑的代码
- vendor.xxx.js：第三方模块代码

而对于 app.xxx.js 文件，如果我们写的js代码特别多的话，那么这个文件就会特别大，非常不利于后期维护，并且难易加载，因而用户在使用系统时，很可能会出现网页短暂空白的情况。

所以**我们可以把不同路由对应的组件分割成不同的代码块，然后当路由被访问的时候才加载对应的组件，这样就更高效了**。这就是<font color=red>路由懒加载</font>

具体方法：一个路由打包成一个 js 文件，只有某个路由被访问到的时候，再去服务器请求对应的组件，而不是一次请求全部的组件。

步骤：

- 修改 /router/index.js 文件中，组件的导入方式即可

  ![image-20221109140148473](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221109140148473.png)

- 之后重新打包，就会发现 /dist/js 文件夹内多了几个 js 文件，这些正是使用路由懒加载打包的三个组件

  ![image-20221109140401019](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221109140401019.png)

### 路由的嵌套

嵌套路由是一种很常见的功能

- 比如在 home 页面中，我们希望通过 /home/news 和 /home/message 访问一些内容
- 一个路径映射一个组件，访问这两个路径也会分别渲染两个组件

实现路由嵌套有两个步骤：

- 创建对应的子组件，并且在路由映射中配置对应的子组件

  - 给组件 Home 创建两个子组件

    ![image-20221109151230439](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221109151230439.png)

  - 在路由映射中配置对应的子组件

    ![image-20221109151420570](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221109151420570.png)

    > children属性是一个数组，用于给组件添加子组件的路由映射关系
    >
    > 子组件的 path 路径前可以不用写 /

- 组件内部使用`<router-view>` 标签

  ```html
  <div id="home">
    <h2>我是首页</h2>
    <p>我是首页内容，哈哈哈</p>
    <router-link to="/home/news" replace>新闻</router-link>
    <router-link to="/home/message" replace>消息</router-link>
    <router-view></router-view>
  </div>
  ```

  ![image-20221109152027402](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221109152027402.png)

### 传递参数的方式

- 传递参数主要有两种类型：params 和 query

- params 类型：
  - 配置路由格式：<font color=red>/router/:id</font>
  - 传递的方式：<font color=red>在 path 后面跟上对应的值</font>
  - 传递后形成的路径 <font color=red>/router/123，/router/abc</font>

- query 类型：

  - 配置路由格式：<font color=red>/router</font>，也就是普通的配置

     ![image-20221109162435845](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221109162435845.png)

  - 传递的方式：对象中使用 <font color=red>query 的 key 作为传递方式</font>

    ![image-20221109162511668](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221109162511668.png)

  - 传递后形成的路径：<font color=red>/router?id=123，/router?id=abc</font>

     ![image-20221109162537626](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221109162537626.png)

  > 如果想要在组件中拿到这个参数，并且使用的是 query 类型，可以通过 `$route.query`获取
  >
  > ![image-20221109162754423](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221109162754423.png)
  >
  > ![image-20221109162817566](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221109162817566.png)

  > 注意点：一般如果有大量数据需要传输的话就选择 query 的方式

#### 传递参数的方式（手动修改代码的方式跳转）

- 在 App.vue 组件中

![image-20221109163741120](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221109163741120.png)

- 定义点击函数

  ![image-20221109163832244](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221109163832244.png)

- 在 Profile.vue 组件中，获取参数

  ![image-20221109163941448](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221109163941448.png)

效果：![image-20221109164027746](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221109164027746.png)



### 导航守卫

#### 为什么使用导航守卫？

**导航守卫可以监听路由跳转的过程**

首先来考虑一个需求：在一个 SPA 应用中，如何改变网页的标题呢？

- 网页标题是通过 `<title>`来显示的，我们可以通过 js 修改 `<title>` 的内容，window.document.title = '新的标题'

而在 Vue 中可以怎么实现呢？

- 方法一（不推荐）：可以通过生命周期中的 create 钩子函数，修改 `<title>`内容；每个组件在被创建出来的时候都会调用 create 函数里面的内容，于是可以在函数内部定义 `document.title = '标题'`，这样的话，哪个组件定义了这个函数，网页标题就会显示哪个组件内修改的标题

- 方法二（推荐）：使用全局导航守卫，只需监听全局的跳转，具体操作如下：

  ```js
  //  /router/index.js
  
  // 创建 VueRouter 对象,给需要在网页中显示对应标题的路由添加 meta 
  const routes = [
    // 配置路由和组件的映射关系
    {
      path: '/',
      redirect: '/home'     
    },
    {
      path: '/home',
      component: () => import('../components/Home.vue'),
      meta: {
        title: '首页'
      },
      children: [
        {
          path: '',
          redirect: 'news'
        },
        {
          path: 'message',
          component: () => import('../components/HomeMessage.vue')
        },
        {
          path: 'news',
          component: () => import('../components/HomeNews.vue')
        }
      ]
    },
    {
      path: '/about',
      component: () => import('../components/About.vue'),
      meta: {
        title: '关于'
      },
    },
    {
      path: '/user/:userId',
      component: () => import('../components/User.vue'),
        meta: {
          title: '用户'
        },
    },
    {
      path: '/profile',
      component: () => import('../components/Profile'),
        meta: {
          title: '我的'
        },
    }
  ]
  
  //调用路由对象的 beforeEach 方法
  router.beforeEach((to, from, next) => {
      
    document.title = to.meta.title
    //to 和 from：都表示 index.js 文件中的一个个路由，只要给路由添加了 meta 属性就可以将内部的 title 赋值给全局的 title 了 `document.title = to.meta.title`
      
    next()    
    //一旦使用了全局导航守卫，在beforeEach方法内的参数中，一定要调用next() 方法，使程序进行下一步
  })
  ```

  > **注意点**：<font color=red>对于有路由嵌套的组件，使用下面的方式修改全局的 title，否则嵌套的路由标题会是 undefined</font>
  >
  > ```js
  > document.title = to.matched[0].meta.title
  > ```

效果：![image-20221110131000081](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221110131000081.png)![image-20221110131015394](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221110131015394.png)

#### 导航守卫补充

- beforEach() 函数，我们称为前置钩子(hook)函数，这个前置钩子需要主动调用 next()

- afterEach() ：后置钩子，不需要主动调用 next() 

上面我们使用的导航守卫，称为**全局守卫**

还有两种守卫

- **路由独享的守卫**

  - 可以在路由配置中直接定义 `beforeEnter` 守卫，这些守卫与前面的全局前置守卫的参数是一致的

    ![image-20221110151405109](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221110151405109.png)

- **组件内的守卫**

  - 可以在路由组件内直接定义以下路由导航守卫

    ![image-20221110151749070](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221110151749070.png)



### keep-alive 遇见 vue-router

我们从一个组件切换到别的组件，再回来这个组件时，这个组件的状态是没有被保留下来的，例如：

- 如下图，新闻组件是默认展示在首页的，而此时我们点击消息组件，就跳转到了消息的组件内容

​		![image-20221110152245709](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221110152245709.png) ![image-20221110152418275](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221110152418275.png)

- 这时我们切换到关于，再回到首页组件，发现消息组件的展示状态没有被保留,而是回到了默认的新闻组件

  ![image-20221110152621050](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221110152621050.png) ![image-20221110152644259](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221110152644259.png)

#### 1.使用 keep-alive

**keep-alive** 是 Vue 内置的一个组件，可以使被包含的组件保留状态，或避免重新渲染

对于上述需求，就可以使用 `keep-alive` 解决

- 在 App.vue 中 ，使用 `<keep-alive>` 标签包裹 `<router-view>`标签

  ```vue
  <keep-alive>
    <router-view></router-view>
  </keep-alive>
  ```

  > 这里使用`<keep-alive>`的**目的**是，保持路由状态，防止每次进入、出来该组件时都重新创建和销毁

- 在 Home.vue 中

  ```js
  export default {
    name: "Home",
    data() {
      return {
        path: '/home/news'					//这里先定义 path 的初始值
      }
    },
    activated() {    							//这个函数在 进入当前组件时调用
      // console.log(this.path);         
      this.$router.push(this.path)  			//一旦进入当前组件，就会跳转到 path 路径（这个path 已被离开该组件的时候修改，也就是说离开组件前是什么路径，进来组件后就是什么路径）
    },
    beforeRouteLeave(to, from, next) {        //这个函数在 离开当前组件时调用
      //console.log(this.$route.path);      
      this.path = this.$route.path  			//一旦离开当前组件，就会执行这一行代码，也就是将离开前活跃状态时的路径赋值给 path（此时 path 已被修改为离开时的路径）
      next()
    }
  ```

> <font color="blue">activated()</font>：在vue对象存活的情况下，进入当前存在activated()函数的页面时，一进入页面就触发；可用于初始化页面数据等。（拓展知识：而如果在这个函数内定义了跳转的路径，那么就不用给这个组件的子组件添加默认跳转路径了）
>
> <font color=blue>deactivated()</font>：与 activated() 函数相反，当前组件不处于活跃状态时调用的函数
>
> <font color=blue>beforeRouteLeave()</font>：离开当前组件对应的路由，就会触发的函数

> **activated() 和 deactivated() 只有在当前组件保持了状态，使用了 `<keep-alive>`时才有效**

> 注意点：对于 `create()` 和 `destoryed` 这两个生命周期函数，一旦==进入==某个组件时，就会调用这个 create() ，一旦离开某个组件时，就会调用这个组件的 destoryed() ，而且<font color=red>每次进入的某个组件，都会新创建出来的</font>。而<font color=red>使用了 keep-alive 之后，每次进入某个组件之后，就只会调用一次 create()</font>

#### 2.keep-alive 属性介绍

`<keep-alive>`有两个非常重要的属性：

- include：字符串或正则表达式，只有匹配的组件会被缓存

- exclude：字符串或正则表达式，任何匹配的组件都不会被缓存

  - 也就是使用 exclude 属性挂载的组件，在进入或者离开该组件的时候，都会反复调用 create 和 destoryed 生命周期函数

    ![image-20221110194721952](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221110194721952.png)

    > 这里要注意属性exclude内的组件之间不要用空格分开

 

# 6.Vuex 详解

## 1.为什么使用 Vuex

### 1.1单页面状态管理

![image-20221112232419925](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221112232419925.png)

#### 单页面状态管理的实现 

![image-20221112232610786](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221112232610786.png)

### 1.2多页面状态管理

![image-20221112232755910](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221112232755910.png)

## 2.Vuex 的基本使用

### 2.1 Vuex 的安装

Vuex 类似于 Vue-Router 都是插件，所以需要安装

`npm install vuex --save`

### 2.2 Vuex 使用

新建一个 store 文件夹，store 文件夹内创建 index.js 文件，这个文件将用于管理 Vuex 配置相关信息。

- /store/index.js： 导入，安装并创建 vuex（这里注意不是创建 Vuex 对象，而是vuex内的一个 Store 属性）

  ![image-20221112231744530](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221112231744530.png)

- 在 mian.js 入口文件中导入并挂载 Vuex 的 Store 对象

  ![image-20221112232111881](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221112232111881.png)

  > <font color=red>在 Vue 实例中挂载一个对象的话，比如我们的 router，store，那么在 Vue 源码中，都会进行 `Vue.prototype.$router`或者 `Vue.prototype.$store` 这一步操作的，所以在我们的组件中就可以使用这个全局的 `$rouer` 和 `$store`</font>

### 2.3 Vuex 状态管理图例

<img src="https://upload-images.jianshu.io/upload_images/16428911-c0047ed13ba514a1.png?imageMogr2/auto-orient/strip|imageView2/2/format/webp" alt="img" style="zoom:80%;" />

- 我们的组件不推荐直接修改 state 状态，而是头通过修改 mutations 来修改 state；而浏览器有一个插件 Devtools 可以记录 mutation 的状态，但是这个插件只能记录同步操作，如果我们的组件有异步操作的话，可以通过 actions 提交

##### 简单案例

![image-20221114112108665](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221114112108665.png)

- 新建一个 store 文件夹，在里面创建 index.js 文件用于存放 vuex 相关操作

  ```js
  //index.js
  import Vue from 'vue'
  import Vuex from 'vuex'
  
  // 1.安装插件
  Vue.use(Vuex)
  
  // 2.创建并导出 store 对象
  export default new Vuex.Store({
    state: {                  //用于保存状态
      counter: 1000
    },
    mutations: {
      // 方法 
      increment(state) {       //一旦调用了mutations里面的方法，就会给这些方法自动传入一个state，这样就可以修改state里面的数据
        state.counter++     
      },
      decrement(state) {
        state.counter--
      }
    }
  })
  ```

- 将 vuex 中的 store 挂载到 Vue 实例中，这样在其他组件中，我们就可以通过 this.$store 的方式，获取到这个对象了

  ```js
  import Vue from 'vue'
  import App from './App.vue'
  import store from './store'
  
  Vue.config.productionTip = false
  
  new Vue({
    store,
    render: h => h(App)
  }).$mount('#app')
  ```

- 使用 vuex 中的 counter

  ```vue
  <template>
    <div id="app">
      <h2>{{$store.state.counter}}</h2>
      <button @click="addition">+</button>
      <button @click="subtracton">-</button>
      <h2><hello-vuex></hello-vuex></h2>
    </div>
  </template>
  
  <script>
  import HelloVuex from "./components/HelloVuex.vue"
  
  export default {
    name: 'App',
    components: {
      HelloVuex
    },
    methods: {
      addition() {
        // 在组件中修改mutatiions需要通过commit方法找到定义的方法
        this.$store.commit('increment')
      },
      subtracton() {
        this.$store.commit('decrement')
      }
    }
  }
  </script>
  
  <style>
  </style>
  ```

演示：![image-20221114113304809](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221114113304809.png)

## 3.Vuex 核心概念

Vuex 中几个比较核心的概念： 

- State：存放需要被多个视图管理的状态（数据），在别的组件只需要使用 $store.state即可访问到里面的数据
- Getters：类似于组件中的计算属性
- Mutations：在这里进行写一些方法，用于修改state中的数据
- Action：进行相关的异步操作
- Module：划分不同的模块，针对不同的模块，再做一些相关数据的保存

#### State单一状态树

- Vuex 提出使用单一状态树，也可以翻译成单一数据源

![image-20221114115704963](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221114115704963.png)

![image-20221114120526300](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221114120526300.png)

> 简单说就是在我们的 Vue 项目中，我们只需要建一个 store 来管理我们的状态

#### Getters基本使用

- 有时候，我们需要从 store 中获取一些 state 变异后的状态，比如下面的 store 中：

  ![image-20221114122526837](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221114122526837.png)

- 在组件中访问：

  ![image-20221114122731232](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221114122731232.png)

- 效果：

  ![image-20221114122611109](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221114122611109.png)

> <font color=blue>getters 就类似于组件中的 computed ，对一个数据或者状态进行修改后再使用就可以使用 getters，在 getters 中定义函数时，也会默认传入一个 **state**</font>		

##### 拓展：

**需求1:**上述代码中，如果要拿到 students 中年龄大于20的对象的长度，可以通过如下方式：

- ![image-20221114124201672](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221114124201672.png)

  > getters 中函数的参数同时也可以拿到getters自身，这样就可以对在函数中修改getters中的函数

- 组件中使用：

  ![image-20221114124316557](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221114124316557.png)

- 效果：

  ![image-20221114124333299](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221114124333299.png)

**需求2:** 动态获取 $store.state.students 内的对象，比如用户传入一个 age ，我们实现从  $store.state.students 中筛选出大于这个 age 的对象，具体操作如下：

- getters 中定义一个函数，函数中再返回一个函数，在这个函数中定义相关操作，并且传入一个 age 形参

  ![image-20221114125148973](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221114125148973.png)

- 组件中传入一个具体的 age

  ![image-20221114125428437](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221114125428437.png)

  > 上面的操作其实就是调用 getters 中的函数，并动态传入参数

#### Mutations 状态更新

- Vuex 的 state 状态的唯一更新方式：**提交Mutation**

- Mutation 主要包括两部分：

  - 字符串的**事件类型**
  - **一个回调函数**，该回调的第一个参数就是 state

  ![image-20221114130212796](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221114130212796.png)

##### 1.Mutations 传递参数

- 在通过 mutation 更新数据时，有可能要携带一些**额外的参数**	
- 这些参数被称为 mutation 的负载（playload）

具体演示代码如下：

```vue
<!--App.vue-->

<template>
  <div id="app">
    <h2>App中的counter：{{$store.state.counter}}</h2>
    <button @click="addcount(5)">+5</button>
    <button @click="addcount(10)">+10</button>
    <button @click="addstudent">添加</button>
  </div>
</template>

<script>
export default {
  name: 'App',
  methods: {
    addcount(count) {
      this.$store.commit('increcount', count)	//用户自己传入一个count
    },
    addstudent() {
      const stu = {id: 4, name: '莱昂纳多', age: 40}
      this.$store.commit('increstu', stu)	 //用户自己定义一个对象并传入
    }
  }
}
</script>

<style>
</style>

```

```js
mutations: {
  increcount(state, count) {	//每次调用，使state中的counter加count的数，count为用户传入的数
    state.counter += count
  },
  increstu(state, stu) {	//每次调用，使state中的students增加一个对象stu，stu为用户定义好的数据
    state.students.push(stu)
  }
},
```

演示：![image-20221114133120157](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221114133120157.png)

- 如果参数不是一个：
  - 这个时候可以以对象的形式传递，也就是说 Payload是一个对象
  - 然后再从对象中取出相关信息

##### 2.Mutations 另一种提交风格

- 之前 Mutation 的提交风格都是下面这种放哪格式：

![image-20221114133924407](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221114133924407.png)

- Mutation 的另一种提交风格就是将 Payload 设置为一个对象，如下：

  ![image-20221114134355682](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221114134355682.png)

  - 那么在 mutations 中传入参数时也要注意通过 `对象.属性`  的方式拿到负载的参数

    ![image-20221114134649031](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221114134649031.png)

- 演示：![image-20221114134839231](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221114134839231.png)

##### 3.Mutation 响应规则

- Vuex的store中的state是响应式的，当state中的数据发生改变时，Vue组件会自动更新.

- 这就必须遵守一些 vuex 对应的规则

  - 提前在 store 中初始化好所需的属性

  - 当给 state 中的对象添加属性时，用下面的方式

    - 方式一：使用 `Vue.set(obj, 'newinfo', 123)`

      ![image-20221115105554296](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221115105554296.png) ![image-20221115105613319](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221115105613319.png)

      > 在 Vuex 中使用 `obj.info['newobj']` 的方式添加新属性是行不通的，页面将不会响应式地发生改变，但是可以修改属性值可以 `state.info.name = 'Iverson'`

    - 方式二：用心对象给旧对象重新赋值

  - 当删除 state 中的对象中的属性时，使用 `Vue.delete(obj, 'oldinfo')`

    ![image-20221115105648845](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221115105648845.png)![image-20221115105800146](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221115105800146.png)

##### Mutation 常量类型 - 代码

![image-20221115110505367](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221115110505367.png)

我们在提交Mutation 这一步骤的时候，经常要来回切换文件，赋值事件类型名称，非常麻烦，且效率低。也就是下面这种情况：

![image-20221115110620783](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221115110620783.png)	![image-20221115110659181](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221115110659181.png)

vuex 提出可以在 store 文件夹下新建一个 mutations_types.js 文件，将 Mutation 的事件类型统一添加到这一文件中作为对象，给组件和 mutations 使用，操作如下：

![image-20221115113613404](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221115113613404.png)

![image-20221115113728908](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221115113728908.png)

![image-20221115113858976](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221115113858976.png)

效果：同样生效

![image-20221115113930891](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221115113930891.png)

##### Mutation 同步函数

![image-20221115114522922](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221115114522922.png)

假如我们直接在 Mutation 中添加异步操作，如下代码：

![image-20221115114832361](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221115114832361.png)

演示：

![image-20221115115041572](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221115115041572.png)

**因此，禁止在 mutations 中写异步操作相关的代码**

#### Action 的基本定义

接上一个 mutations 中只能定义同步函数的问题，可以使用 Actions 替代其进行异步操作

具体使用如下：

![image-20221115120457345](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221115120457345.png)

- 在 actions 中定义异步操作

![image-20221115120508889](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221115120508889.png)

- 组件中，通过 dispatch 提交至 actions

![image-20221115120638570](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221115120638570.png)

- 演示：

![image-20221115120911311](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221115120911311.png)

**如果 actions 中完成了提交，我们希望告诉组件提交成功，我们可以用下面的方式：**

- /store/index.js 中：我们可以给事件类型返回一个 Promise对象，当提交给 mutations 成功后，我们调用 resolve函数，并且传入一些需要返回给组件的数据

  ![image-20221115122056992](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221115122056992.png)

- 在组件中：我们可以调用前面 actions 中函数返回的 Promise对象的 then() 方法，对成功的结果做一个处理，响应给组件

  ![image-20221115122023548](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221115122023548.png)

补充一下 Vuex 状态管理图例：

<img src="https://upload-images.jianshu.io/upload_images/16428911-c0047ed13ba514a1.png?imageMogr2/auto-orient/strip|imageView2/2/format/webp" alt="img" style="zoom:80%;" />

#### Modules 基本使用

 <img src="C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221115122840827.png" alt="image-20221115122840827" style="zoom: 67%;" />

具体使用如下：

- 在 /store/index.js 中的 store 给 modules 定义一个模块

  ![image-20221115124522624](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221115124522624.png)

- 组件中提交给 mutations 和前面的一致

  ![image-20221115124619589](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221115124619589.png)

- 打印：![image-20221115124635406](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221115124635406.png)

  ![image-20221115124658772](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221115124658772.png)

> 给 modules 中的 getters 添加的函数，在使用时，与之前的同样类似

##### 模块中的 getters 使用

- 在模块中getters的函数内定义一些代码，如下：

![image-20221115125908309](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221115125908309.png)

- 演示：

![image-20221115130011320](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221115130011320.png)

- 打印：

  ![image-20221115130028604](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221115130028604.png)

#### 项目结构

Vuex 中的所有的核心概念，官方推荐将除 state 的代码外其他的全都抽成一个文件，而 modules 抽成一个文件夹，这样做更方便管理。

演示：如右图					![image-20221115131329996](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221115131329996.png)



# 7.axios

**axios：ajax i/o system**

**功能特点：**

- 在浏览器中发送 XMLHttpRequests 请求
- 在 node.js 中发送 http 请求
- 支持 Promise API
- 拦截请求和响应
- 转换请求和响应数据
- 等等

### axios 请求方式

支持多种请求方式：

- axios(config)
- axios.request(config)
- axios.get(url[, onfig])
- axios.delete(url[, onfig])
- axios.head(url[, data[, onfig]])
- axios.delete(url[, onfig])
- axios.put(url[, data[, config]])
- axios.patch(url[, data[.,config]])

### axios 基本使用

- 安装 axios

  `npm i axios --save`

- 在某个 js 文件中导入并使用

  ```js
  import axios from 'axios'
  
  axios({
    url: 'http://123.207.32.32:8000/home/multidata',
  }).then((res) => {	//axios支持Promise API，所以可以直接调用then()方法
    console.log(res);
  })
  ```

  > 如果没有指定请求方式，默认是 GET 请求



### axios 发送并发请求

- 使用`axios.all()` 这个 API 就可以发送多个请求
- all() 方法内传入的是一个数组，可以将多个 axios 传入这个数组中。
- axios([]) 返回的是一个数组，使用 axios.spread 可将叔祖 [res1, res2] 展开为 res1，res2

- 具体操作如下：

```js
axios.all([axiois({
  url: 'http://123.207.32.32:8000/home/multidata'
}),axios({
  url: 'http://123.207.32.32:8000/home/data',
  params: {
    type: 'sell',
    page: 1
  }
})]).then(res => {
  console.log(red)
})

//如果要将两个返回的结果展开，而不是使用索引的方式得到数组中的数据，使用下面的方式
axios.all([axiois({
  url: 'http://123.207.32.32:8000/home/multidata'
}), axios({
  url: 'http://123.207.32.32:8000/home/data',
  params: {
    type: 'sell',
    page: 1}})])
.then(axios.spread((res1, res2) => {
  console.log(res1)
  console.log(res1)
}))
```



### 全局配置

![image-20221116152040915](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221116152040915.png)

#### 常见的配置选项

![image-20221116152639381](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221116152639381.png)



### axios 实例

有的时候我们的项目会变得比较复杂，为了处理并发的问题，我们需要将不同的接口地址分给不同的服务器，而且每个服务器都有各自的 ip 地址，那么我们配置全局的地址，超时时间等就不合适了，也就是下面的情况。

**![image-20221116153645009](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221116153645009.png)**

解决方法：创建对应的 axios 的实例

```js
//创建对应的 axios 的实例

//第一个axios的实例
const instance1 = axios.create({
  baseURL: 'http://123.207.32.32:8000',
  timeout: 5000  
})

instance1({
  url: '/home/multidata'
}).then(res => {
  console.log(red)  
})

instance1({
  url: '/home/data',
  params: {
    type: 'pop',
    page: 1  
  }
}).then(res => {
  console.log(red)  
})

//第二个axios的实例
const instance2 = axios.create({
  baseURL: 'http://127.0.0.1:8080',
  timeout: 10000  
})
...
```



### axios 模块封装

假如不使用模块封装，也就是在使用网络请求的组件中直接导入 axios 模块并使用，代码如下：

```vue
<template>
  <div id="app">
    <p>{{result}}</p>
  </div>
</template>

<script>
import axios from 'axios'		//导入

export default {
  name: 'App',
  data() {
    return {
      result: ''
    }
  },
  components: {
  },
  created() {
    axios({
      url: 'http://123.207.32.32:8000/home/multidata'
    }).then(res => {
      this.result = res
    })
  }
}
</script>

<style>
</style>
```

打印：![image-20221116160637332](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221116160637332.png)

对于上面这种使用 axios 的方式看似也可以实现，但是要考虑几个问题，首先每个组件如果都要使用 axios 的话，需要每个组件逐一导入 axios 模块，我们建议组件中不要过于依赖模块，并且假如 axios 有一天不维护了，那么，就需要去每个组件中修改对应的代码，非常的不利于我们开发，所以我们需要将 axios 模块进行封装使用

**具体操作：**

- 新建一个 network 文件夹，文件夹新建 request.js 文件，以后所有关于网络请求的内容都写在这个 js 里面

  **写法一：**

  - request.js 文件

    ```js
    //request.js
    
    import axios from 'axios'
    
    export function request(config, success, failure) {
      // 1.创建 axios 实例
      const instance = axios.create({
        baseURL: 'http://123.207.32.32:8000',
        timeout: 5000
      })
    	
      instance(config).then(res => {
        success(res)
      }).catch(err => {
        failure(err)
      })
    }
    ```

  - 组件中使用：

    ```js
    import {request} from './network/request'
    
    request({
      url: '/home/multidata'
    }, res => {
      console.log(res);
    }, err => {
      console.log(err);
    })
    ```

  - 打印：

    ![image-20221116163152872](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221116163152872.png)

  

  **写法二：**

  - request.js 文件

    ```js
    //request.js
    
    import axios from 'axios'
    
    export function request(config) {
      // 1.创建 axios 实例
      const instance = axios.create({
        baseURL: 'http://127.0.0.1:8080',
        timeout: 5000
      })
    	
      instance(config.baseUrl).then(res => {
        config.success(res)
      }).catch(err => {
        config.failure(err)
      })
    }
    ```

  - 组件中使用：

    ```js
    import {request} from './network/request'
    
    request({
      baseUrl: '/home/multidata',
      success: (res) => {
        console.log(res)
      },
      failure: (err) => {
        console.log(err)
      }
    })
    ```

  **写法三（推荐）：**

  - request.js

    ```js
    export function request(config) {
      return new Promise((resolve, reject) => {
        // 1.创建 axios 实例
        const instance = axios.create({
          baseURL: 'http://123.207.32.32:8000',
          timeout: 5000
        })
    
        instance(config)
          .then(res => {
            resolve(res)
          })
          .catch(err => {
            reject(err)
          })
      })
    }
    ```

  - 组件中使用：

    ```js
    request({
      url:'/home/multidata',
    }).then(res => {
      console.log(res);
    }).catch(err => {
      console.log(err);
    })
    ```

  **写法四（推荐使用）：**

  - request.js

    ```js
    export function request(config) {
        // 1.创建 axios 实例
        const instance = axios.create({
          baseURL: 'http://123.207.32.32:8000',
          timeout: 5000
        })
    
        return instance(config)   //直接return，因为我们实例化的instance本身就是一个 Promise
    }		
    ```

  - 组件中使用：

    ```js
    request({
      url:'/home/multidata',
    }).then(res => {
      console.log(res);
    }).catch(err => {
      console.log(err);
    })
    ```

    

### axios 拦截器

- axios 提供了拦截器，用于我们在发送每次请求或者得到响应后，进行对应的处理

- 如何使用拦截器？

  ![image-20221116183256289](C:\Users\DuMer\AppData\Roaming\Typora\typora-user-images\image-20221116183256289.png)

**具体使用：**

拦截分==请求拦截==和==响应拦截==

- /network/request.js

  ```js
  import axios from 'axios'
  export function request(config) {
    // 1.创建 axios 实例
    const instance = axios.create({
      baseURL: 'http://123.207.32.32:8000',
      timeout: 5000
    })
  
    // 2. axios 的请求拦截器
    // 	2.1 拦截请求
    instance.interceptors.request.use(config => {
      // console.log(config);
      // (1)比如在拦截器中，可以将不属于服务器要求的数据进行一些修改
      //  config 
      // (2)比如每次发送网络请求时，都希望在界面中显示一个请求的图标
  
      // (3)某些网络请求(比如登录(token))，必须携带一些特殊的信息
      return config         //进行了拦截操作一定要记住，将传进来的 config 返回出去
    }, err => {
      console.log(err);
    })
  
    // 	2.2 拦截响应
    instance.interceptors.response.use(res => {
      // console.log(res);
      return res.data   //这里可以指定返回的是响应结果中的 data 数据
    }, err => {
      console.log(err);
    })
  
    // 3.发送真正的网络请求
    return instance(config)
  }
  ```

- 组件中使用：

  ```js
  import {request} from './network/request'
  request({
    url:'/home/multidata',
  }).then(res => {
    console.log(res);
  }).catch(err => {
    console.log(err);
  })
  ```

  