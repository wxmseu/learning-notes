##### vue的特点

- 采用组件化模式，提高代码复用率、且让代码更好维护
- 声明式编码，让编码人员无需直接操作DOM，提高开发效率
- 使用虚拟DOM+优秀的Diff算法，尽量复用DOM节点。

##### 前置js基础

- es6语法规范
- es6模块化
- 包管理器
- 原型、原型链
- 数组常用方法
- axios
- promise

##### 1.初识vue

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script type="text/javascript" src="../js/vue.js"></script>
    <title>初识vue</title>
</head>
<body>
<!--
    初识vue：
    1. 想让vue工作，就必须创建一个vue实例，且要传入一个配置对象
    2. root容器里的代码依然符合html规范，只不过混入了一些特殊的vue语法；
    3. root容器里的代码被称为【vue模板】；
    4. vue实例和容器是一一对应的；
    5. 真是开发中只有一个vue实例，并且会配合着组件一起使用
    6. {{xxx}} 中的xxx要写js表达式，且xxx可以自动读取到data中的所有属性；
    7. 一旦data中的数据发生改变，那么模板中用到该数据的地方也会自动更新；
-->
<!-- 准备好一个容器-->
<div id="root">
    <h1>hello,{{name}}</h1>
    <h1>我的年龄,{{age}}</h1>
    <hr>
    <!--v-bind:可以简写为:-->
    <!--
    vue模板语法有两大类
    1. 插值语法：
        功能：用于解析标签体内容
        写法：{{xxx}} 中的xxx要写js表达式，且xxx可以自动读取到data中的所有属性；
    2. 指令语法：
        功能：用于解析标签（包括：标签属性标签体内容、绑定事件。。。。）
        备注：vue中有很多指令，形式都是v-xxx
    -->
    <a v-bind:href='url' v-bind:x="hello">点击去百度一下</a>
</div>
<script type="text/javascript">
    Vue.config.productionTip = false
    // 创建Vue实例
    new  Vue({
        // el用于指定当前vue实例为哪个容器服务，值通常为css选择器字符串
        el:'#root',
        // data中用于存储数据，数据供el所指定的容器去使用，值我们暂时先写成一个对象
        data:{
            name:'wxm',
            age:'18',
            url:'http://www.baidu.com',
        }
    })
</script>
</body>

</html>
```

##### 2.模板语法

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script type="text/javascript" src="../js/vue.js"></script>
    <title>初识vue</title>
</head>
<body>

<div id="root">
    <!--v-bind:可以简写为:-->
    <!--
    vue模板语法有两大类
    1. 插值语法：
        功能：用于解析标签体内容
        写法：{{xxx}} 中的xxx要写js表达式，且xxx可以自动读取到data中的所有属性；
    2. 指令语法：
        功能：用于解析标签（包括：标签属性标签体内容、绑定事件。。。。）
        备注：vue中有很多指令，形式都是v-xxx
    -->
    <a v-bind:href='url.toUpperCase()' v-bind:x="hello">点击去等一下{{school.name}}</a>
</div>
<script type="text/javascript">
    Vue.config.productionTip = false
    // 创建Vue实例
    new  Vue({
        // el用于指定当前vue实例为哪个容器服务，值通常为css选择器字符串
        el:'#root',
        // data中用于存储数据，数据供el所指定的容器去使用，值我们暂时先写成一个对象
        data:{
            name:'wxm',
            age:'18',
            url:'http://www.baidu.com',
            school:{
                name:'jdq',
                gender:'女'
            }
        }
    })
</script>
</body>

</html>
```

##### 3.数据绑定

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script type="text/javascript" src="../js/vue.js"></script>
    <title>初识vue</title>
</head>
<body>
<!--
    vue中有2种数据绑定的方式：
        1. 单向绑定（v-bind)：数据只能从data流向页面。
        2. 双向绑定（v-model）：数据不仅能从data流向页面，还可以从页面流向data
        备注：
            1. 双向绑定一般都应用在表单元素类上（如input，select）
            2. v-model：value可以简写成v-model，因为v-model默认收集 的就是value值
-->
<div id="root">
    <!--普通写法-->
    单向数据绑定<input type="text" v-bind:value="msg"></br>
    双向数据绑定<input type="text" v-model:value="msg"></br>

     <!--简写-->
     单向数据绑定<input type="text" :value="msg"></br>
     双向数据绑定<input type="text" v-model="msg"></br>
    <!--一下代码为错误，因为v-model只能应用在表单类元素（输入类元素）-->
    <h2 v-model:x="msg">你好啊</h2>
</div>
<script type="text/javascript">
    // 创建Vue实例
    new  Vue({
        el:'#root',
        data:{
            name:'wxm',
            age:'18',
            url:'http://www.baidu.com',
            school:{
                name:'jdq',
                gender:'女'
            },
            msg:'hello world'
        }
    })
</script>
</body>

</html>
```

##### 4.el和data写法

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <!--引入vue-->
    <script type="text/javascript" src="../js/vue.js"></script>
    <title>初识vue</title>
</head>
<body>
<!-- 
    data与el的两种写法
    1. el有两种写法：
        1. new vue 的时候配置el属性
        2. 先创建vue实例，随后再通过v.$mount('root')指定el 的值
    2. data有两种写法
        1. 对象式
        2. 函数式
        如何选择：目前都可以，等之后用到组件时，data必须用函数式，否则就会报错。
    3. 重要原则：
         由vue管理的函数，一定不要写箭头函数(()=>),一旦写了箭头函数，this就不再是vue实例了。
-->
<div id="root">
    <h1>hello,{{name}}</h1>
</div>
<script type="text/javascript">
    // 创建Vue实例
    // el的两种写法
    // const v=new  Vue({
    //     // el的第一种方式
    //     // el:'#root',
    //     data:{
    //         name:'wxm',
    //         age:'18',
    //         url:'http://www.baidu.com',
    //     }
    // })
    // console.log(v)
    // // el的第二种方式mount 挂载
    // v.$mount('#root')

    // data的两种写法
    // data'的第一种写法：对象式 
    // data:{
    //         name:'wxm',
    //         age:'18',
    //         url:'http://www.baidu.com',
    //     }
    const v=new  Vue({
        el:'#root',
        // data的第二种写法： 函数式
        data(){
            console.log('---',this) //此处的this是vue的实例对象
            return{
                name:'wxm'
            }
        }
    })
    
</script>
</body>

</html>
```

##### 5.MVVM模型

```vue
MVVM模型：
1. M:模型（model）：data中的数据
2. V:视图（view）：模板代码
3. VM：视图模型（ViewModel）：vue实例
观察发现：
1. data中的所有属性，最后都出现在了vm身上
2. vm身上所有的属性及vue原型上所有属性，在vue模板中都可以直接使用

```

##### 6.数据代理

###### 1.Object.defineproperty方法

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script type="text/javascript" src="../js/vue.js"></script>
    <title>回顾Object.defineproperty方法</title>
</head>
<body>

<script type="text/javascript">
    let number=18
    let person={
        name:'wxm',
        gender:'man',
    }
    Object.defineProperty(person,'age',{
        // value:18,
        // enumerable:true,//控制属性是否可以枚举，默认为false
        // writable:true,//控制属性是否可以被修改，默认为false
        // configurable:true, //控制属性是否可以被删除，默认为false

        // 当有人读取person的age属性时，get函数(getter)就会被调用，且返回值就是age的值
        get(){
            console.log("有人读取了age的值")
            return number
        },

        // 当有人修改person的age属性时i，set函数（setter）就会被调用，且会收到修改的具体值
        set(value){
            console.log("有人修改了age属性，且值是",value)
            number=value
        }
    })
    console.log(person)
    // console.log(Object.keys(person))

</script>
</body>

</html>
```

###### 2.何为数据代理

数据代理：通过一个对象代理对另一个对象中属性的操作 读/写

```js
let obj1={x:100}
let obj2={y:200}
Object.defineProperty(obj2,'x',{
    get(){
        return obj1.x
    },
    set(value){
        obj1.x=value
    }
})
```

###### 3.vue中数据代理

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script type="text/javascript" src="../js/vue.js"></script>
    <title>Document</title>
</head>
<body>
    <!--
        vue中的数据代理：
        1. 通过vm对象来代理data对象中属性的操作（读/写）
        2. 好处：更加方便的操作data中的数据
        3. 基本原理
            通过Object.defineproperty()把data对象中所有属性添加到vm上
            为每一个添加到vm上的属性，都指定一个getter/setter
            在getter/setter内部去操作（读/写）data中对应的属性
    -->
    <div id="root">
        <h1>学校名称：{{name}}</h1>
        <h1>学校地址：{{address}}</h1>
    </div>
<script type="text/javascript">
    const vm = new Vue({
        el:'#root',
        data:{
            name:'wxm',
            address:'苏州市'
        }
    })
</script>
</body>
</html>
```

![image-20230107153720566](C:\Users\xiaom\AppData\Roaming\Typora\typora-user-images\image-20230107153720566.png)

![image-20230107153841995](C:\Users\xiaom\AppData\Roaming\Typora\typora-user-images\image-20230107153841995.png)

由图中可以看到在vm中添加了name和address属性，来代理获取修改_data中的属性。

_data作了数据劫持，为了作响应式。

##### 7.事件处理

###### 1.事件的基本使用

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script type="text/javascript" src="../js/vue.js"></script>
    <title>Document</title>
</head>
<body>
    <!--
       事件的基本使用：
       1. 使用v-on：xxx或者@xxx绑定事件，其中xxx是事件名字
       2. 事件的回调需要配置在methods对象中，最终会在vm上
       3. methods中配置的函数，不要用箭头函数，否则this就不为vm而是window
       4. methods中配置的函数，都是被vue所管理的函数，this的指向是vm或组件实例对象
       5. @click='demo'和@click='demo($event)'效果一致，但后者可以传参
    -->
    <div id="root">
        <h1>热烈欢迎{{name}}同学前来学习</h1>
        <button v-on:click="showInfo1">点我提示信息1(不传参）</button>
        <button v-on:click="showInfo2(number,$event)">点我提示信息2（传参）</button>
    </div>
<script type="text/javascript">
    const vm = new Vue({
        el:'#root',
        data:{
            name:'jdq',
            address:'苏州市'
        },
        methods:{
            showInfo1(event){
                alert('欢迎同学')
                // console.log(event.target.innerText)
                // console.log(this) // 此处的this是vm
            },
            showInfo2(number){
                alert('欢迎同学!!')

            },
        }
    })
</script>
</body>
</html>
```

###### 2.事件装饰符

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script type="text/javascript" src="../js/vue.js"></script>
    <title>Document</title>
    <style>
        *{
            margin: 20px;
        }
        .demo1{
            height: 50px;
            background-color: burlywood;
        }
        .box1{
            padding: 5px;
            background-color: aqua;
        }
        .box2{
            background-color:skyblue;
        }
        .list{
            width: 200px;
            height: 200px;
            background-color: palegoldenrod;
            overflow: auto;
        }
        li{
            height: 100px;
        }

    </style>
</head>
<body>
    <!--
        vue中的事件修饰符：
        1. prevent：阻止默认事件（常用）
        2. stop：阻止事件冒泡（常用）
        3. once：事件只触发一次（常用）
        4. capture：使用事件的捕获模式
        5. self：只有event.target是当前操作的元素时才触发事件
        6. passive：事件的默认行为立即执行，无需等待事件回调执行完毕

    -->
    <div id="root">
        <h1>热烈欢迎{{name}}同学前来学习</h1>
        <!-- prevent为事件的修饰符，阻止默认行为 -->
        <a href="https:www.baidu.com" @click.prevent="showinfo">点我提示信息</a>

        <!-- stop：阻止事件冒泡（常用） -->
        <div class="demo1" @click="showinfo">
            <!-- <button @click.stop="showinfo">点我提示信息</button> -->
            <!-- 修饰符可以连着写 -->
            <a href="https:www.baidu.com" @click.stop.prevent="showinfo">点我提示信息</a>
        </div>

        <!-- once：事件只触发一次（常用） -->
        <button @click.once="showinfo">点我提示信息</button>

        <!-- capture：使用事件的捕获模式，捕获为由外到内，冒泡是由内到外-->
        <div class="box1" @click.capture="showmsg(1)">
            div1
            <div class="box2" @click="showmsg(2)">
                div2
            </div>
        </div>

        <!-- self：只有event.target是当前操作的元素时才触发事件 -->
        <div class="demo1" @click.self="showinfo2">
            <button @click="showinfo2">点我提示信息</button>
        </div>

        <!-- passive：事件的默认行为立即执行，无需等待事件回调执行完毕 -->
        <!-- scroll:是滚动条的滚动事件，可以是鼠标滚轮或者键盘的上下键，wheel指的是鼠标滚轮的滚动 -->
        <ul @wheel.passive="demo" class="list">
        <!-- <ul @scroll="demo" class="list"> -->
            <li>1</li>
            <li>2</li>
            <li>3</li>
            <li>4</li>

        </ul>
    </div>
<script type="text/javascript">
    const vm = new Vue({
        el:'#root',
        data:{
            name:'jdq',
        },
        methods:{
            showinfo(){
                alert('同学你好')
            },
            showinfo2(){
                console.log(event.target)
            },
            showmsg(msg){
                alert(msg)
            },
            demo(){
                // console.log('@')
                for(let i =0;i<100000;i++){
                    console.log('#')
                };
                console.log('累坏了')
            }
        }
    })
</script>
</body>
</html>
```

###### 3.键盘事件

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="../js/vue.js"></script>
    <title>键盘事件</title>
</head>
<body>
    <!-- 
        1.vue中的常用的按键别名：
            回车：enter
            删除：delete（捕获‘删除’和‘退格’键）
            退出：esc
            空格：space
            换行：tab   (特殊，需配合keydown)
            上：up
            下：down
            左：left
            右：right
        2. vue中未提供别名的按键，可以使用按键原始的key值去绑定，但注意要转为kebab-case（短横线命名）
            例如:大小写键 cap-lock
        3. 系统修饰键（用法特殊）：ctrl、alt、shift、meta
            1. 配合keyup使用：按下修饰键的同时，再按下其他键，随后释放其他键，事件才被触发
            2. 配合keydown使用：正常触发事件
        
        4. 也可以使用keyCode去指定具体的按键（不推荐）

        5. Vue.config.keyCodes.自定义按键名=键码，可以定制按键别名
     -->
    <div id="root">
        <h1>欢迎{{name}}来学习</h1>
        <!-- 键盘事件的别名也可以连着写 -->
        <input type="text" placeholder="按下回车提示输入" @keyup.ctrl.y="showinfo">
    </div>
    <script>
        Vue.config.keyCodes.huiche=13
        const vm=new Vue({
            el:'#root',
            data(){
                return{
                    name:'jdq',

                }
            },
            methods: {
                showinfo(e){
                    // console.log(e.target.value)
                    // console.log(e.key,e.keyCode)//keycode表示按下键盘的编码
                    console.log(e.target.value)
                }
            },
        })
    </script>
</body>
</html>
```

##### 8.计算属性

###### 1.姓名案例_插值语法实现

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="../js/vue.js"></script>
    <title>计算属性</title>
</head>
<body>
    <!-- 
     
     -->
    <div id="root">
        姓：<input type="text" v-model="lastname"> <br>
        名：<input type="text" v-model="firstname"> <br>
        全名：<span>{{lastname.slice(0,3)}}-{{firstname}}</span>
    
    </div>
    <script>
        const vm=new Vue({
            el:'#root',
            data(){
                return{
                    lastname:'张',
                    firstname:'三'
                }
            },
            methods: {
               
            },
        })
    </script>
</body>
</html>
```

###### 2.姓名案例_methods实现

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="../js/vue.js"></script>
    <title>计算属性</title>
</head>
<body>
    <!-- 
     
     -->
    <div id="root">
        姓：<input type="text" v-model="lastname"> <br>
        名：<input type="text" v-model="firstname"> <br>
        全名：<span>{{fullname()}}</span>
    
    </div>
    <script>
        Vue.config.productionTip = false
        const vm=new Vue({
            el:'#root',
            data(){
                return{
                    lastname:'zhang',
                    firstname:'san'
                }
            },
            methods: {
                fullname(){
                    // data中的任何一个数据发生变化，模板都会重新解析，效率不高
                    res=this.lastname+'-'+this.firstname
                    res.toUpper()
                    return res
                }
            }
        })
    </script>
</body>
</html>
```

###### 3.姓名案例_计算属性实现

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="../js/vue.js"></script>
    <title>计算属性</title>
</head>
<body>
    <!-- 
        计算属性：
            1. 定义：要用的属性不存在，要通过已有的属性计算得来
            2. 原理：底层借助了object.defineproperty方法提供的getter和setter
            3. get函数什么时候被调用
                1. 初次读取的时候 
                2. 所依赖的数据发生变化时会再次调用
            4. 优势：与methods实现相比，内部有缓存机制（复用），效率更高，调试方便
            5. 备注
                1. 计算属性最终会出现在vm中，直接读取即可
                2. 如果计算属性要被修改，那必须写set函数去响应修改，且set中要引起计算所依赖的属性发生变化

     -->
    <div id="root">
        姓：<input type="text" v-model="lastname"> <br>
        名：<input type="text" v-model="firstname"> <br>
        全名：<span>{{fullname}}</span>
    
    </div>
    <script>
        Vue.config.productionTip = false
        const vm=new Vue({
            el:'#root',
            data(){
                return{
                    lastname:'zhang',
                    firstname:'san'
                }
            },
            computed:{
                fullname:{
                    // get的作用：当有人读取fullname的时候，get就会被调用，且返回值作为fullname的值
                    // get什么时候被调用？1. 初次读取fullname的时候 2. 所依赖的数据发生变化时
                    get(){
                        console.log('@get被调用了')

                        return this.lastname+'-'+this.firstname
                    },
                    // set什么时候被调用？ 当fullname被修改的时候
                    set(value){
                        this.lastname=value.split('-')[0]
                        this.firstname=value.split('-')[1]
                    },
                },
            }
        })
    </script>
</body>
</html>
```

###### 4.姓名案例_计算属性简写

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="../js/vue.js"></script>
    <title>计算属性</title>
</head>
<body>
    <!-- 
     -->
    <div id="root">
        姓：<input type="text" v-model="lastname"> <br>
        名：<input type="text" v-model="firstname"> <br>
        全名：<span>{{fullname}}</span>
    
    </div>
    <script>
        Vue.config.productionTip = false
        const vm=new Vue({
            el:'#root',
            data(){
                return{
                    lastname:'zhang',
                    firstname:'san'
                }
            },
            computed:{
                // 计算属性完整写法
                // fullname:{
                //     get(){
                //         console.log('@get被调用了')
                //         return this.lastname+'-'+this.firstname
                //     },
                //     set(value){
                //         this.lastname=value.split('-')[0]
                //         this.firstname=value.split('-')[1]
                //     },
                // },
                // 简写，在确定计算属性只包含get时，不包括set
                fullname(){
                    console.log('@get被调用了')
                    return this.lastname+'-'+this.firstname
                }
            },
        })
    </script>
</body>
</html>
```

##### 9.监视属性

###### 1.天气案例

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script src="../js/vue.js"></script>
    <title>监视属性</title>
</head>
<body>
    <!-- 
     -->
    <div id="root">
        <h2>今天的天很{{info}}</h2>
        <button @click="changeweather">切换天气</button>
    </div>
    <script>
        Vue.config.productionTip = false
        const vm=new Vue({
            el:'#root',
            data(){
                return{
                    ishot:true,
                }
            },
            computed:{
                info(){
                    return this.ishot ? '炎热':'凉爽'
                }
            },
            methods:{
                changeweather(){
                    return this.ishot=!this.ishot
                }
            },
        })
    </script>
</body>
</html>
```

###### 2.监视属性

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script src="../js/vue.js"></script>
    <title>监视属性</title>
</head>
<body>
    <!--  
        监视属性：
            1. 当被监视的属性变化时，回调函数自动调用，进行相关操作
            2. 监视的属性必须存在，才能进行监视
            3. 监视的两种写法：
                1. new Vue时传入watch配置
                2. vm.$watch监视
     -->
    <div id="root">
        <h2>今天的天很{{info}}</h2>
        <button @click="changeweather">切换天气</button>
    </div>
    <script>
        Vue.config.productionTip = false
        const vm=new Vue({
            el:'#root',
            data(){
                return{
                    ishot:true,
                }
            },
            // 计算属性
            computed:{
                info(){
                    return this.ishot ? '炎热':'凉爽'
                }
            },
            // 事件方法
            methods:{
                changeweather(){
                    return this.ishot=!this.ishot
                }
            },
            // 监视属性
            watch:{
                // 既可以监视data中的属性，也可以监视计算属性
                ishot:{
                    immediate:true, // 初始化时让handler调用，默认为false
                    // handler什么时候被调用？ 当ishot改变时
                    handler(newvalue,oldvalue){
                        console.log('ishot被修改了',newvalue)
                    }
                },
                // info:{
                //     immediate:true, // 初始化时让handler调用，默认为false
                //     // handler什么时候被调用？ 当ishot改变时
                //     handler(newvalue,oldvalue){
                //         console.log('info被修改了',newvalue)
                //     }
                // },
            }
        })
        // 或者采用这种方式进行监视，watch中有两个参数，第一个为监视的属性，第二个为配置
        vm.$watch('info',{
            handler(newvalue,oldvalue){
                console.log('info被修改了',newvalue)
            }
        })
    </script>
</body>
</html>
```

###### 3.深度监视

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script src="../js/vue.js"></script>
    <title>监视属性</title>

</head>
<body>
    <!--  
        深度监视：
            1. vue中的watch默认不检测对象内部值的变化（一层）
            2. 配置deep：true可以监视对象内部值的变化（多层）
        备注：
            1. vue自身可以检测内部值的变化，但vue提供的watch不支持
            2. 使用watch时根据数据的具体结构，决定是否采用深度监视。
    
     -->
    <div id="root">
        <h2>今天的天很{{info}}</h2>
        <button @click="changeweather">切换天气</button>
        <hr/>
        <h3>a的值为{{numbers.a}}</h3>
        <button @click="numbers.a++">点我让a增加1</button>
        <hr/>
        <h3>b的值为{{numbers.b}}</h3>
        <button @click="numbers.b++">点我让b增加1</button>
    </div>
    <script>
        Vue.config.productionTip = false
        const vm=new Vue({
            el:'#root',
            data(){
                return{
                    ishot:true,
                    numbers:{
                        a:1,
                        b:2
                    }
                }
            },
            computed:{
                info(){
                    return this.ishot ? '炎热':'凉爽'
                }
            },
            methods:{
                changeweather(){
                    return this.ishot=!this.ishot
                }
            },
            watch:{
                ishot:{
                    handler(newvalue,oldvalue){
                        console.log('ishot被修改了',newvalue)
                    }
                },
                // 监视多级结构中某个属性的变化
                'numbers.a':{
                    handler(){
                        console.log('a被修改了')
                    }

                },
                // 监视多级结构中所有属性的变化
                numbers:{
                    // 深度监视
                    deep:true,
                    handler(){
                        console.log('numbers被修改了')
                    }

                },
              
            }
        })
     

    </script>
</body>
</html>
```

###### 4.监视属性简写

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script src="../js/vue.js"></script>
    <title>监视属性</title>

</head>
<body>
    <!--  
     -->
    <div id="root">
        <h2>今天的天很{{info}}</h2>
        <button @click="changeweather">切换天气</button>

    </div>
    <script>
        Vue.config.productionTip = false
        const vm=new Vue({
            el:'#root',
            data(){
                return{
                    ishot:true,
                }
            },
            computed:{
                info(){
                    return this.ishot ? '炎热':'凉爽'
                }
            },
            methods:{
                changeweather(){
                    return this.ishot=!this.ishot
                }
            },
            // watch:{
                // ishot:{
                //     //正常写法
                //     deep:true,
                //     immediate:true,
                //     handler(newvalue,oldvalue){
                //         console.log('ishot被修改了',newvalue)
                //     }

                // },
                
                // 简写，配置项只有handler时可以简写
                // ishot(newvalue,oldvalue){
                //     console.log('ishot被修改了',newvalue)
                // }
              
            // }
        })

        // 对于通过通过vm.$watch的监视写法按如下简写形式，也是只配置handler项
        vm.$watch('ishot',function(newvalue,oldvalue){
            console.log('ishot被修改了',newvalue)
        })

    </script>
</body>
</html>
```

5.watch和computed的区别

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="../js/vue.js"></script>
    <title>watch监视实现08中的姓名案例</title>
</head>
<body>
    <!-- 
        watch和computed的区别：
            1. computed能完成的，watch都能完成
            2. watch能完成的，computed不一定能完成，比如watch能完成异步任务
        两个重要的小原则：
            1. 所被vue管理的函数，最好写成普通函数，这样this的指向才是vm或者是组件实例对象
            2. 所有不被vue管理的函数（定时器的回调函数，ajax的回调函数等），最好写成箭头函数，
               这样this 的指向才是vm或者是组件实例对象
     -->
    <div id="root">
        姓：<input type="text" v-model="lastname"> <br>
        名：<input type="text" v-model="firstname"> <br>
        全名：<span>{{fullname}}</span>
    
    </div>
    <script>
        Vue.config.productionTip = false
        const vm=new Vue({
            el:'#root',
            data(){
                return{
                    lastname:'zhang',
                    firstname:'san',
                    fullname:'zhang-san'
                }
            },
            watch:{
                lastname(newvalue){
                    setTimeout(() => {
                        this.fullname=newvalue+'-'+this.firstname
                    }, 1000);   
                },
                firstname(newvalue){
                    this.fullname=this.lastname+'-'+newvalue
                }
            }

        })
    </script>
</body>
</html>
```

##### 10.绑定样式

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script src="../js/vue.js"></script>
    <title>绑定样式</title>
    <style>
        .basic{
            border: 30px;
        }
        .happy{
            border: 30px;
            background-color: aquamarine;
        }
        .sad{
            border-radius: 5px;
        }
        .excited{
            font-size: 40px;
        }
    </style>
</head>
<body>
    <!-- 
    
     -->
    <div id="root">
        <!-- 绑定class样式--字符串写法，适用于：样式的类名不确定，需要动态指定 -->
        <div class="basic" :class='mood' @click="changemotion">{{name}}</div><br><br>

        <!-- 绑定class样式--数组写法，适用于：要绑定的样式个数不确定，名字也不确定 -->
        <div class="basic" :class='arr'>{{name}}</div><br><br>

        <!-- 绑定class样式--对象写法，适用于：要绑定的样式个数确定，名字确定，动态决定 -->
        <div class="basic" :class='classObj'>{{name}}</div><br><br>

        <!-- 绑定style样式--对象写法 -->
        <div class="basic" :style="styleObj1">{{name}}</div><br><br>   

        <!-- 绑定style样式--数组写法 -->
        <div class="basic" :style="[styleObj1,styleObj2]">{{name}}</div><br><br>   
    </div>
    <script>
        Vue.config.productionTip = false
        const vm=new Vue({
            el:'#root',
            data:{
                name:'wxm',
                mood:'happy',
                arr:['happy','sad','excited'],
                classObj:{
                    'happy':false,
                    'excited':false
                },
                styleObj1:{
                    fontSize:'50px',
                    backgroundColor:'orange',
                },
                styleObj2:{
                    color:'blue'
                }
            },
            methods: {
                changemotion(){
                    var arr=['happy','sad','excited']
                    var  i =Math.floor(Math.random()*3)
                    while (arr[i]===this.mood) {
                        i =Math.floor(Math.random()*3)
                    }
                   
                    this.mood=arr[i]
                    console.log('心情改变了为:',this.mood)
                }
            },
        })
    </script>
</body>
</html>
```

##### 11.条件渲染

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script src="../js/vue.js"></script>
    <title>条件渲染</title>
</head>
<body>
    <!-- 
        条件渲染：
        1.v-if
            写法：
                1. v-if="表达式"
                2. v-else-if="表达式"
                3. v-else="表达式"
            适用于：切换频率较低的场景
            特点：不展示的DOM元素直接被移除
            注意：v-if可以和：v-else-if、v-else一起使用，但结构不能被打断
        2. v-show
            写法：v-show="表达式"
            适用于：切换频率较高的场景
            特点：不展示的DOM元素未被移除，仅是使用样式隐藏掉

        3. 备注：使用v-if时，元素可能无法获取到，而使用v-show一定可以获取到
     -->
    <div id="root">
        <!-- 使用v-show作条件渲染，是通过调节style中的dispaly属性来实现的 -->
        <h2 v-show='view'>欢迎来到{{name}}</h2>

        <!-- 使用v-if作条件渲染，区域块将不在页面上显示-->
        <h3 v-if='view'>欢迎来到{{name}}</h3>

        <h3>当前的n值为{{n}}</h3>
        <button @click="n++">点我n+1</button>
        <!-- v-show作条件渲染 -->
        <div v-show="n==1">react</div>
        <div v-show="n==2">auj</div>
        <div v-show="n==3">vue</div>
        <br><br>
        <!-- v-if-else作渲染 -->
        <div v-if="n==1">react</div>
        <div v-else-if="n==2">auj</div>
        <div v-else-if="n==3">vue</div>
        <div v-else>haha</div>

        <!-- v-if 与template配合使用，不能使用v-show-->
        <template v-if="n===1">
            <div >你好</div>
            <div >北京</div>
            <div >！</div>
        </template>
        



    </div>
    <script>
        Vue.config.productionTip = false
        const vm=new Vue({
            el:'#root',
            data(){
                return{
                    name:'我的世界',
                    view:true,
                    n:0
                }
            },
        })
    </script>
</body>
</html>

```

##### 12.列表渲染

###### 1.基本列表

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script src="../js/vue.js"></script>
    <title>列表渲染</title>
</head>
<body>
    <!-- 
        v-for指令：
            1. 用于展示列表数据
            2. 语法：v-for="(item,index) i xxx" :key='index'
            3. 可遍历数组、对象、字符串（用的少）、指定次数（用的少）

     -->
    <div id="root">
        <!-- 遍历数组 -->
        <h2>人员信息</h2>
        <ul>
            <li>姓名-年龄</li>
            <!-- <li v-for="person in persons" :key="person.id">{{person.name}}-{{person.age}}</li> -->
            <li v-for="(person,index) in persons" :key="index">
                {{person.name}}-{{person.age}}
            </li>
        </ul>

        <!-- 遍历对象 -->
        <h2>汽车信息</h2>
        <ul>
            <!-- 注意：第一个为值v，第二个为键k -->
            <li v-for="(v,k) in car" :key="k">{{k}}--{{v}}</li>
        </ul>

        <!-- 遍历字符串 -->
        <h2>字符串信息（用的少）</h2>
        <ul>
            <li v-for="(v,index) in str" :key="index">{{v}}--{{index}}</li>
        </ul>

        <!-- 遍历指定次数 -->
        <h2>遍历指定次数（用的少）</h2>
        <ul>
            <li v-for="(n,index) in 8" :key="index">{{n}}--{{index}}</li>
        </ul>

    </div>
    <script>
        const vm=new Vue({
            el:'#root',
            data:{
                persons:[
                    {id:123,name:'张三',age:17},
                    {id:124,name:'李四',age:18},
                    {id:125,name:'王五',age:19},
                ],
                car:{
                    name:'奥迪',
                    price:23,
                    color:'black'
                },
                str:'helllo'
            }
        })
    </script>
</body>
</html>

```

###### 2.key的原理

![image-20230110164811425](C:\Users\xiaom\AppData\Roaming\Typora\typora-user-images\image-20230110164811425.png)

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script src="../js/vue.js"></script>
    <title>列表渲染</title>
</head>
<body>
    <!-- 
        面试题：react、vue中的key有什么作用？（key的内部原理）
            1. 虚拟DOM中key的作用
                key是虚拟DOM对象的标识，当状态中的数据发生变化时，vue会根据【新数据】生成【新的虚拟DOM】，
                随后vue进行【新虚拟DOM】与【旧虚拟DOM】的差异比较，比较规则如下：
            2. 对比规则
                1. 旧虚拟DOM中找到了与新虚拟DOM相同的key：
                    1. 若虚拟DOM中内容没变, 直接使用之前的真实DOM！
                    2. 若虚拟DOM中内容变了, 则生成新的真实DOM，随后替换掉页面中之前的真实DOM。
                2. 旧虚拟DOM中未找到与新虚拟DOM相同的key：
                    创建新的真实DOM，随后渲染到到页面。
                3. 用index作为key可能会引发的问题：
                    1. 若对数据进行：逆序添加、逆序删除等破坏顺序操作:
                        会产生没有必要的真实DOM更新 ==> 界面效果没问题, 但效率低。
                    2. 如果结构中还包含输入类的DOM：
                        会产生错误DOM更新 ==> 界面有问题。
                4. 开发中如何选择key?:
                    1.最好使用每条数据的唯一标识作为key, 比如id、手机号、身份证号、学号等唯一值。
                    2.如果不存在对数据的逆序添加、逆序删除等破坏顺序操作，仅用于渲染列表用于展示，
                        使用index作为key是没有问题的。
     -->
    <div id="root">
        <!-- 遍历数组 -->
        <h2>人员信息</h2>
        <button @click.once="addPerson">添加一个老六</button>
        <ul>
            <li>姓名-年龄</li>
            <!-- <li v-for="person in persons" :key="person.id">{{person.name}}-{{person.age}}</li> -->
            <li v-for="(person,index) in persons" :key="person.id">
                {{person.name}}-{{person.age}}
                <input type="text">
            </li>
        </ul>

    </div>
    <script>
        const vm=new Vue({
            el:'#root',
            data:{
                persons:[
                    {id:123,name:'张三',age:17},
                    {id:124,name:'李四',age:18},
                    {id:125,name:'王五',age:19},
                ],
            },
            methods: {
                addPerson(){
                    var p={id:126,name:'老六',age:19}
                    this.persons.unshift(p)

                }
            },
        })
    </script>
</body>
</html>

```

###### 3.列表过滤

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script src="../js/vue.js"></script>
    <title>列表渲染</title>
</head>
<body>
    <!-- 
     -->
    <div id="root">
        <h2>人员信息</h2>
        <input type="text" placeholder="要搜索的人" v-model="keyWord">
        <ul>
            <li>姓名-年龄</li>
            <li v-for="person in filPersons" :key="person.id">
                {{person.name}}-{{person.age}}
            </li>
        </ul>

    </div>
    <script>
        // 用监视属性watch实现
        /* const vm=new Vue({
            el:'#root',
            data:{
                keyWord:'',
                persons:[
                    {id:123,name:'马冬梅',age:17,gender:'women'},
                    {id:124,name:'周冬雨',age:18,gender:'women'},
                    {id:125,name:'周杰伦',age:19,gender:'man'},
                    {id:125,name:'温兆伦',age:19,gender:'man'},
                ],
                filPersons:[]
            
            },
            watch:{
                keyWord:{
                    immediate:true,
                    handler(val){
                        this.filPersons=this.persons.filter((p)=>{
                        return p.name.indexOf(val)!==-1
                        })
                    }
                }
            }
        }) */
        // 用计算属性computed实现
        const vm=new Vue({
            el:'#root',
            data:{
                keyWord:'',
                persons:[
                    {id:123,name:'马冬梅',age:17,gender:'women'},
                    {id:124,name:'周冬雨',age:18,gender:'women'},
                    {id:125,name:'周杰伦',age:19,gender:'man'},
                    {id:125,name:'温兆伦',age:19,gender:'man'},
                ],
            },
            computed:{
                filPersons(){
                    return this.persons.filter((p)=>{
                        return p.name.indexOf(this.keyWord)!==-1
                    })
                }
            }
        })
    </script>
</body>
</html>

```

###### 4.列表排序

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script src="../js/vue.js"></script>
    <title>列表渲染</title>
</head>
<body>
    <!-- 
     -->
    <div id="root">
        <h2>人员信息</h2>
        <input type="text" placeholder="要搜索的人" v-model="keyWord">
        <button @click="sortType=2">年龄升序</button>
        <button @click="sortType=1">年龄降序</button>
        <button @click="sortType=0">默认顺序</button>
        <ul>
            <li>姓名-年龄</li>
            <li v-for="person in filPersons" :key="person.id">
                {{person.name}}-{{person.age}}
            </li>
        </ul>

    </div>
    <script>
        // 用计算属性computed实现
        const vm=new Vue({
            el:'#root',
            data:{
                keyWord:'',
                sortType:0, // 0 原顺序 1 降序 2 升序
                persons:[
                    {id:'123',name:'马冬梅',age:17,gender:'women'},
                    {id:'124',name:'周冬雨',age:18,gender:'women'},
                    {id:'125',name:'周杰伦',age:19,gender:'man'},
                    {id:'126',name:'温兆伦',age:19,gender:'man'},
                ],
            },
            computed:{
                filPersons(){
                    const arr= this.persons.filter((p)=>{
                        return p.name.indexOf(this.keyWord)!==-1
                    })
                    // 判断是否需要排序
                    if(this.sortType){
                        arr.sort((p1,p2)=>{
                            return this.sortType===1 ? p2.age-p1.age : p1.age-p2.age
                        })
                    }
                    return arr
                }
            }
        })
    </script>
</body>
</html>

```

5.vue更新数据时的一个问题

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script src="../js/vue.js"></script>
    <title>列表渲染</title>
</head>
<body>
    <!-- 
     -->
    <div id="root">
        <h2>人员信息</h2>
        <button @click="updateMei">点击更新马冬梅</button>
        <ul>
            <li>姓名-年龄</li>
            <li v-for="person in persons" :key="person.id">
                {{person.name}}-{{person.age}}--{{person.gender}}
            </li>
        </ul>

    </div>
    <script>
        // 用计算属性computed实现
        const vm=new Vue({
            el:'#root',
            data:{
                keyWord:'',
                sortType:0, // 0 原顺序 1 降序 2 升序
                persons:[
                    {id:'123',name:'马冬梅',age:17,gender:'women'},
                    {id:'124',name:'周冬雨',age:18,gender:'women'},
                    {id:'125',name:'周杰伦',age:19,gender:'man'},
                    {id:'126',name:'温兆伦',age:19,gender:'man'},
                ],
            },
            methods:{
                updateMei(){
                    // 奏效的写法
                    // this.persons[0].name='马老师' 
                    // this.persons[0].age=40
                    // 不奏效的写法
                    this.persons[0]={id:'123',name:'马老师',age:40,gender:'women'}
                }
            }
        })
    </script>
</body>
</html>

```

###### 5.更新时的一个问题

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script src="../js/vue.js"></script>
    <title>列表渲染</title>
</head>
<body>
    <!-- 
     -->
    <div id="root">
        <h2>人员信息</h2>
        <button @click="updateMei">点击更新马冬梅</button>
        <ul>
            <li>姓名-年龄</li>
            <li v-for="person in persons" :key="person.id">
                {{person.name}}-{{person.age}}--{{person.gender}}
            </li>
        </ul>

    </div>
    <script>
        // 用计算属性computed实现
        const vm=new Vue({
            el:'#root',
            data:{
                keyWord:'',
                sortType:0, // 0 原顺序 1 降序 2 升序
                persons:[
                    {id:'123',name:'马冬梅',age:17,gender:'women'},
                    {id:'124',name:'周冬雨',age:18,gender:'women'},
                    {id:'125',name:'周杰伦',age:19,gender:'man'},
                    {id:'126',name:'温兆伦',age:19,gender:'man'},
                ],
            },
            methods:{
                updateMei(){
                    // 奏效的写法
                    // this.persons[0].name='马老师' 
                    // this.persons[0].age=40
                    // 不奏效的写法
                    // this.persons[0]={id:'123',name:'马老师',age:40,gender:'women'}
                    // 正确的写法
                    this.persons.splice(0,1,{id:'123',name:'马老师',age:40,gender:'women'})
                }
            }
        })
    </script>
</body>
</html>

```

###### 6.Vue监测数据改变的原理_对象

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script src="../js/vue.js"></script>
    <title>列表渲染</title>
</head>
<body>
    <!-- 
     -->
    <div id="root">
        <h2>学校名称：{{name}}</h2>
        <h2>学校地址：{{address}}</h2>
    

    </div>
    <script>
    const vm=new Vue({
        el:'#root',
        data:{
            name:'wxm',
            address:'苏州市'
        }
    })
    </script>
</body>
</html>

```

###### 7.模拟一个数据监测

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>

</head>
<body>
    <script type="text/javascript">
        let data={
            name:'wxm',
            address:'苏州市'
        }
        // 创建一个监测的实例对象，用于监视data中属性的变化
        const obs=new Observer(data)
        console.log(obs)
        let vm={}
        vm._data=obs

        function  Observer(obj){
            // 汇总数据中的所有属性形成一个数组
            const keys=Object.keys(obj)
            keys.forEach((k)=>{
                Object.defineProperty(this,k,{
                    get(){
                        console.log(`${k}被调取了`)
                        return obj[k]
                    },
                    set(val){
                        console.log(`${k}被修改了，我要去解析模板，生成虚拟DOM了`)
                        obj[k]=val
                    },
                })
            })
        }
    </script>
</body>
</html>
```

###### 8.Vue.set的使用

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script src="../js/vue.js"></script>
    <title>列表渲染</title>
</head>
<body>
    <!-- 
     -->
    <div id="root">
        <h2>名称：{{school.name}}</h2>
        <h2>地址：{{school.address}}</h2>
        <h2 v-show="school.leader">校长：{{school.leader}}</h2>
        <button  @click="addMaster">点我添加校长</button>

        <hr>
        <h2>姓名：{{student.name}}</h2>
        <button @click="addGender">点我添加性别，默认为男</button>
        <h2 v-show="student.gender">性别：{{student.gender}}</h2>
        <h2>年龄：真实年龄-{{student.age.rAge}},对外年龄-{{student.age.sAge}}</h2>
        <h2>朋友们</h2>
        <ul>
            <li v-for="f in student.friends" :key="f.name">姓名{{f.name}}--年龄{{f.age}}</li>
        </ul>

    </div>
    <script>
    const vm=new Vue({
        el:'#root',
        data:{
            school:{
               name:'wxm',
            address:'苏州市', 
            },

            
            student:{
                name:'tom',
                age:{
                    rAge:40,
                    sAge:18,
                },
                friends:[
                    {name:'jerry',age:35},{name:'tim',age:29}
                ]
            }
        },
        methods: {
            addGender(){
                this.$set(this.student,'gender','男')
                // Vue.set(this.student,'gender','男')
            },
            addMaster(){
                this.$set(this.school,'leader','漂亮的小季')
            }
        },
    })
    </script>
</body>
</html>

```

###### 9.Vue监测数据改变的原理_数组

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script src="../js/vue.js"></script>
    <title>列表渲染</title>
</head>
<body>
    <!-- 
     -->
    <div id="root">
        <h2>名称：{{school.name}}</h2>
        <h2>地址：{{school.address}}</h2>
        <h2 v-show="school.leader">校长：{{school.leader}}</h2>
        <button  @click="addMaster">点我添加校长</button>

        <hr>
        <h2>姓名：{{student.name}}</h2>
        <button @click="addGender">点我添加性别，默认为男</button>
        <h2 v-show="student.gender">性别：{{student.gender}}</h2>
        <h2>年龄：真实年龄-{{student.age.rAge}},对外年龄-{{student.age.sAge}}</h2>
        <h2>朋友们</h2>
        <ul>
            <li v-for="f in student.friends" :key="f.name">姓名{{f.name}}--年龄{{f.age}}</li>
        </ul>
        <h2>爱好</h2>
        <ul>
            <li v-for="h in student.hobby" :key="h">{{h}}</li>
        </ul>
        <button @click="changeHobby">点我改变爱好，将打篮球改为打踢足球</button>

    </div>
    <script>
    const vm=new Vue({
        el:'#root',
        data:{
            school:{
               name:'wxm',
            address:'苏州市', 
            },
            student:{
                name:'tom',
                age:{
                    rAge:40,
                    sAge:18,
                },
                friends:[
                    {name:'jerry',age:35},{name:'tim',age:29}
                ],
                hobby:['打游戏','跑步','打篮球']
            }
        },
        methods: {
            addGender(){
                this.$set(this.student,'gender','男')
                // Vue.set(this.student,'gender','男')
            },
            addMaster(){
                this.$set(this.school,'leader','漂亮的小季')
            },
            changeHobby(){
                // 以下写法都可以
                // Vue.set(this.student.hobby,2,'踢足球')
                // this.$set(this.student.hobby,2,'踢足球')
                this.student.hobby.splice(2,1,'踢足球')
            }
        },
    })
    </script>
</body>
</html>

```

###### 10.Vue数据监测_总结

```vue
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <!--! 引入vue -->
    <script src="../js/vue.js"></script>
</head>

<body>
    <!-- 
        Vue监视数据的原理：
        1. Vue会监视data中所有层级的数据
        2. 如何监测对象中的数据：
            通过setter实现监测，且要在new Vue时就传入要监测的数据
            1. 对象中后追加的属性，Vue默认不做响应式处理
            2. 如需给后添加的属性做响应式，请使用如下API：
                Vue.set(target,propertyName/index,value)或vm.$set(target,propertyName/index,value)
        3. 如何监测数组中的数据？
            通过包裹数组更新元素的方法实现，本质就是做了两件事：
            1. 调用原生对应的方法对数组进行更新
            2. 重新解析模板，进而更新页面
        4. 在Vue中更新数组中的某个元素一定要用如下方法：
            1. 使用这些API：push(),pop(),shift(),unshift(),splice(),sort(),reverse()
            2. Vue.set()或vm.$set()
        
        特别注意：Vue.set和vm.$set()不能给vm或者vm的根数据对象添加属性。
     -->
    <!--! 容器 -->
    <div id="root">
        <h2>name：{{people.name}}</h2>
        <!--? age -->
        <div class="box">
            <button @click="addAge">addAge</button>
            <h2>age：{{people.age}}</h2>
        </div>
        <!--? sex -->
        <div class="box">
            <button @click="addSex">addSex</button>
            <h2 v-if="people.sex">sex：{{people.sex}}</h2>
        </div>
        <!--? hobbies -->
        <div class="box">
            <button @click="addHobby">addHobby</button>
            <button @click="editFirstHobby">editFirstHobby</button>
            <h2>hobbies：</h2>
            <ul>
                <li v-for="(hobby,index) in people.hobbies" :key="index">
                    hobby{{index+1}}：{{hobby}}
                </li>
            </ul>
        </div>
        <!--? friends -->
        <div class="box">
            <button @click="addFriendInFront">addFriendInFront</button>
            <button @click="editFirstFriend">editFirstFriend</button>
            <h2>friends</h2>
            <ul>
                <li v-for="(friend,index) in people.friends" :key="index">
                    friend{{index+1}}：{{friend.name}} -- {{friend.age}}
                </li>
            </ul>
        </div>
    </div>
</body>

<script>
    // 以阻止 vue 在启动时生成生产提示。
    Vue.config.productionTip = false

    // 创建vue实例
    const vm = new Vue({
        el: '#root',
        data: {
            people: {
                name: 'yahoo',
                age: 23,
                hobbies: ['抽烟', '喝酒', '烫头'],
                friends: [{
                    name: 'BonZi',
                    age: 23
                }, {
                    name: 'Rose',
                    age: 24
                }]
            }
        },
        methods: {
            addAge() {
                this.people.age++
            },
            addSex() {
                // 方法一：
                this.$set(this.people, 'sex', 'boy')
                // 方法二：
                // Vue.set(this.people, 'sex', 'boy')
            },
            addHobby() {
                this.people.hobbies.push('skate')
            },
            editFirstHobby() {
                // 方法一：
                this.people.hobbies.splice(0, 1, '滑板')
                // 方法二：
                // this.$set(this.people.hobbies, 0, '滑板')
                // 方法三：
                // Vue.set(this.people.hobbies, 0, '滑板')
            },
            addFriendInFront() {
                const cabbage = {
                    name: 'cabbage',
                    age: 22
                }
                this.people.friends.unshift(cabbage)
            },
            editFirstFriend() {
                this.people.friends[0].name = 'lover'
            }
        },
    })
</script>

</html>

```

##### 13.收集表单数据

```vue
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <!--! 引入vue -->
    <script src="../js/vue.js"></script>
</head>
<!-- 
    收集表单数据：
        若<input type="text/password"> 则v-model收集的是value值，用户输入的就是value值
        若<input type="radio"> 则v-model收集的是value值，且要给标签配置value值
        若<input type="checkbox">：
            1. 没有配置input的value属性，那么就是收集的checked（勾选or未勾选，是布尔值）
            2. 配置了input的value属性
                1. v-model的初始值是非数组，那么收集的就是checked （勾选or未勾选，是布尔值）
                2. v-model的初始值是数组，那么收集的就是value组成的数组
        备注：v-model的三个修饰符：
            lazy：失去焦点再收集数据
            number：输入字符串转为有效的数字
            trim：输入首尾空格过滤
 -->
<body>
    <!-- 
     -->
    <!--! 容器 -->
    <div id="root">
        <form @submit.prevent="demo">
            账号：<input type="text" v-model.trim="account"><br><br>
            密码：<input type="password" v-model="password"><br><br>
            性别：
            男<input type="radio" name="gender" v-model="gender" value="男">
            女<input type="radio" name="gender" v-model="gender" value="女"><br><br>
            年龄<input type="number" v-model.number="age"><br><br>
            爱好：
            打篮球<input type="checkbox" value="打篮球" v-model="hobby">
            踢足球<input type="checkbox" value="踢足球" v-model="hobby">
            打游戏<input type="checkbox" value="打游戏" v-model="hobby"><br><br>
            所属校区：
            <select v-model="city">
                <option value="">请选择校区</option>
                <option value="beijing">北京</option>
                <option value="shanghai">上海</option>
                <option value="shenzhen">深圳</option>
                <option value="wuhan">武汉</option>
            </select><br><br>
            其他信息：
            <textarea v-model.lazy="others"></textarea>
            <br><br>
            <input type="checkbox" v-model="isAgree">
            阅读并接受<a href="https:www.baidu.com">《用户协议》</a>
            <br><br>
            <button>提交</button>

        </form>
    </div>
</body>

<script>
    const vm = new Vue({
        el: '#root',
        data: {
            account:'',
            password:'',
            gender:'',
            age:'',
            hobby:[],
            city:'',
            others:'',
            isAgree:false,
        },
        methods: {
            demo(){
                alert('提交了')
            }
        },
    })
</script>

</html>

```

##### 14.过滤器

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <script src="../js/vue.js"></script>
    <script src="../js/dayjs.min.js"></script>
</head>
<!-- 

 -->
<body>
    <!-- 
        过滤器：
            定义：对要显示的数据进行特定格式化后再显示（适用于一些简单的逻辑，vue3已弃用）
            语法：
                1. 注册过滤器：Vue.filter(name,function(value){})或者new Vue(filters:{})
                2. 使用过滤器：{{ xxx | 过滤器名 }} 或v-bind：属性=" xxx | 过滤器名"
            备注：
                1. 过滤器也可以接受额外参数，多个过滤器可以串联
                2. 并没有改变原本的数据，是产生新的对应数据。
     -->
    <div id="root">
        <h2>显示当前格式化后的时间</h2>
        <!-- 计算属性实现 -->
        <h2>现在时间是：{{fmtTime}}</h2>

        <!-- methods实现 -->
        <h2>现在时间是：{{getFmtTime()}}</h2>

        <!-- 过滤器实现 -->
        <h2>现在时间是：{{time | timeFormater}}</h2>
        <h2>现在时间是：{{time | timeFormater('YYYY-MM-DD')}}</h2>
        <h2>现在时间是：{{time | timeFormater('YYYY-MM-DD') | myslice}}</h2>
    </div>
    <div id="root2">
        <h2>{{msg|myslice}}</h2>
    </div>
</body>

<script>
    // 全局过滤器
    Vue.filter('myslice',function(v){
        return v.slice(0,4)
    })
    const vm = new Vue({
        el: '#root',
        data: {
            time:1673426312042,
        },
        computed:{
            fmtTime(){
                // dayjs需传入一个时间戳，如果不传入参数，将默认为执行程序时的时间戳
                return dayjs(this.time).format('YYYY-MM-DD HH:mm:ss')
            }
        },
        methods: {
            getFmtTime(){
                return dayjs(this.time).format('YYYY-MM-DD HH:mm:ss')
            }
        },
        // 局部过滤器
        filters:{
            timeFormater(v,str='YYYY-MM-DD HH:mm:ss'){
                return dayjs(v).format(str)
            },
            // myslice(v){
            //     return v.slice(0,4)
            // }
        }
    })
    new Vue({
        el:'#root2',
        data:{
            msg:'hello world'
        }
    })
</script>

</html>

```

##### 15.内置指令

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <script src="../js/vue.js"></script>
    <script src="../js/dayjs.min.js"></script>
    <style>
        [v-cloak]{
            display: none;
        }
    </style>
</head>
<!-- 

 -->
<body>
    <!-- 
        已经学过的内置指令：
            v-bind：单向绑定解析表达式，简写为:xxx
            v-model：双向数据绑定
            v-for：遍历数组、对象、字符串
            v-on：绑定事件监听，简写为@xxx
            v-if：条件渲染
            v-else：条件渲染
            v-show：条件渲染
            v-text:
                1. 作用：向其所在的节点中渲染文本内容
                2. 与插值语法的区别：v-text会替换掉节点的内容，而{{xx}}不会。
            v-html:
                1. 作用：向指定节点中渲染包含html结果的内容
                2. 与插值语法的区别：
                    1. v-html会替换掉节点的内容，而{{xx}}不会。
                    2. v-html可以识别html结构
                3. 注意：v-html有安全性问题：
                    1. 在网站上动态渲染任何HTML是非常危险的，容易导致XSS攻击
                    2. 一定要在可信的内容上使用v-html，永远不要用在用户提交的内容上。
            v-cloak(没有值):
                1. 本质是一个特殊属性，Vue实例创建完毕并接管容器后，会删掉v-cloak属性
                2. 使用css配合v-cloak可以解决网速慢时页面展示出{{xxx}}的问题
            v-once:
                1. v-once所有节点在初次动态渲染后，就视为静态内容
                2. 以后数据的改变不会引起v-once所在结构的更新，可以用于优化性能
            v-pre：
                1. 跳过其所在节点的编译
                2. 可利用它跳过：没有使用指令语法、没有使用插值语法的节点。会加快编译。
            
     -->
    <div id="root">
        <h2>你好，{{name}}</h2>
        <!-- v-text -->
        <h2 v-text="name"></h2>

        <!-- v-html -->
        <h2 v-html="str"></h2>

        <!-- v-cloak -->
        <h2 v-cloak>{{name}}</h2>

        <!-- v-once -->
        <h2 v-once>n的初始值为{{n}}</h2>
        <h2>当前n的值为：{{n}}</h2>
        <button @click="n++">点我n+1</button>

        <!-- v-pre -->
        <h2 v-pre>vue其实很简单</h2>
        <h2>当前的n值是{{n}}</h2>
        <button @click="n++">点我n+1</button>
    </div>
</body>

<script>
    const vm = new Vue({
        el: '#root',
        data: {
            name:'jdq',
            str:'<h3>你好啊</h3>',
            n:1,
        },
        
    })
</script>

</html>

```

##### 16.自定义指令

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>自定义指令</title>
    <script src="../js/vue.js"></script>
    <script src="../js/dayjs.min.js"></script>
    <style>
        [v-cloak]{
            display: none;
        }
    </style>
</head>
<!-- 
    自定义指令总结：
        1. 定义语法
            1. 局部指令：
                new Vue({directives:{指令名：配置对象}})  或者
                new Vue({directives{指令名(){}}})
            2. 全局指令
                Vue.directive('指令名',配置对象)    或者
                Vue.directive('指令名',回调函数)
        
        2. 配置对象中常用的三个回调函数：
            1. bind：指令与元素成功绑定时调用
            2. inserted：指令所在元素被插入到页面时调用
            3. update：指令所在模板结构被重新解析时调用

        3. 备注：
            1. 定义指令时不加v-，但使用时候需要加v-
            2. 指令名如果是多个单词，要使用kebab-case命名方法，不要用cameCase命名。
 -->
<body>
    <!-- 
        需求1： 定义一个v-big指令，和v-text功能类似，但会把绑定的数值放大10倍
        需求2： 定义一个v-fbind指令，和v-bind功能类似，但可以让其绑定的input元素默认获取焦点
     -->
    <div id="root">
        <h2>当前的n值是<span v-text="n"></span></h2>
        <h2>放大后的的n值是<span v-big="n"></span></h2>
        <button @click="n++">点我n+1</button>
        <hr>
        <input type="text" v-bind:value="n">
        <input type="text" v-fbind:value="n">
    </div>
</body>

<script>
    const vm = new Vue({
        el: '#root',
        data: {
            n:1
        },
        directives:{
            // 函数式写法，有两个参数，element，binding
            // big函数何时会被调用？ 1. 元素和指令成功绑定的时候，2. 指令所在的模板被重新解析时
            big(element,binding){
                element.innerText=binding.value*10
                // 此处的this是window
                console.log('big调用了',this)

            },
            // 对象式写法，完整写法
            fbind:{
                // 元素和指令成功绑定的时候调用bind函数
                bind(element,binding){
                    element.value=binding.value
                },
                // 指令所在元素插入页面时调用inserted函数
                inserted(element,binding){
                    element.focus()
                },
                // 指令所在的模板被重新解析时调用update函数
                update(element,binding){
                    element.value=binding.value
                },
            }
        }
    })
</script>

</html>

```

##### 17.生命周期

###### 1.引入生命周期

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>生命周期</title>
    <script src="../js/vue.js"></script>
    <style>
    </style>
</head>
<!-- 
    生命周期：
        1. 又名：生命周期回调函数、生命周期函数、生命周期钩子
        2. 是什么：vue在关键的时间点帮我们调用的一些特殊名称的函数
        3. 生命周期函数的名称不可更改，但是函数的具体内容是根据具体需求编写的
        4. 生命周期函数中的this指向是vm或者组件实例对象
 -->
<body>
    <div id="root">
        <h2 :style="{opacity}">欢迎学习vue</h2>
    </div>
</body>

<script>
    const vm = new Vue({
        el: '#root',
        data: {
            opacity:1,
        }, 
        // Vue完成模板的解析并把初始的真实的DOM放入页面（挂载完毕，即第一次完成挂载）后调用mounted
        mounted() {
            console.log('调用了mounted')
            setInterval(() => {
                this.opacity-=0.01
                if (this.opacity<=0) {
                    this.opacity=1
                }
            }, 16);
        },
    })
    // 通过外部的定时器实现（不推荐）
    /* setInterval(() => {
        vm.opacity-=0.01
        if (vm.opacity<0) {
            vm.opacity=1
        }
    }, 16); */
</script>
</html>
```

###### 2.分析生命周期

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>生命周期</title>
    <script src="../js/vue.js"></script>
    <style>
    </style>
</head>
<!-- 
 -->
<body>
    <div id="root">
        <h2>当前的n值是{{n}}</h2>
        <button @click="add">点我n++</button> 
        <button @click="bye">点我销毁vm</button>
    </div>
    <script>
        const vm = new Vue({
            el: '#root',
            data: {
                n:1,
            }, 
            methods: {
                add(){
                    console.log('add')
                    this.n++
                },
                bye(){
                    console.log('bye')
                    // 完全销毁一个实例(vm)，清理它与其它实例的连接，解绑它的全部指令及事件监听器。
                    // 触发 beforeDestroy 和 destroyed 的钩子。
                    this.$destroy()
                }
            },
           /*  template:`
            <div>
                <h2>当前的n值是{{n}}</h2>
                <button @click="n++">点我n++</button> 
            </div>`, */
            beforeCreate() {
                console.log('before create')
            },
            created() {
                console.log('created')
            },
            beforeMount() {
                console.log('before mounted')
            },
            mounted() {
                console.log('mounted')
            },
            beforeUpdate() {
                console.log('before update')
            },
            updated() {
                console.log('updated')
            },
        })
    </script>
</body>
</html>

```

###### 3.生命周期总结

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>生命周期</title>
    <script src="../js/vue.js"></script>
    <style>
    </style>
</head>
<!-- 
    常用的生命周期钩子：
        1. mounted：发送ajax请求、启动定时器、绑定自定义事件、订阅消息等【初始化操作】
        2. beforeDestroy：清除定时器、解除自定义事件、取消消息订阅等【收尾工作】

    关于销毁vue实例：
        1. 销毁后借助vue开发者工具看不到任何信息
        2. 销毁后自定义事件会失效，但原生DOM事件依然有效
        3. 一般不会在beforeDestroy中操作数据，因为即使操作了数据，也不会再触发更新流程
 -->
<body>
    <div id="root">
        <h2 :style="{opacity}">欢迎学习vue</h2>
        <button @click="stop">点我停止效果</button>
    </div>
</body>

<script>
    const vm = new Vue({
        el: '#root',
        data: {
            opacity:1,
        }, 
        // Vue完成模板的解析并把初始的真实的DOM放入页面（挂载完毕，即第一次完成挂载）后调用mounted
        mounted() {
            console.log('调用了mounted')
            this.timer=setInterval(() => {
                this.opacity-=0.01
                console.log('interval')
                if (this.opacity<=0) {
                    this.opacity=1
                }
            }, 16);
        },
        methods: {
            stop(){
                this.$destroy()
            }
        },
        beforeDestroy() {
            clearInterval(this.timer)
        },
    })
</script>

</html>

```

![image-20230129170740983](C:\Users\xiaom\AppData\Roaming\Typora\typora-user-images\image-20230129170740983.png)

##### 18.非单文件组件

###### 1.基本使用

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>非单文件组件</title>
    <script src="../js/vue.js"></script>
    <style>
    </style>
</head>
<!-- 
    Vue中使用组件的三大步骤：
        1. 定义组件（创建组件）
        2. 注册组件
        3. 使用组件（写组件标签）
    1. 如何定义组件？
        使用Vue.extend(options)创建。其中options和new Vue(options)中的几乎一样，但区别如下：
            1. el不写。原因：最终所有的组件都要经过一个vm的管理，由vm中的el决定服务哪个容器
            2. data必须写成函数式。原因：避免组件被复时，数据存在引用关系
        备注：使用template可以配置组件结构
    2. 如何注册组件
        1. 局部注册，靠new Vue时传入components选项
        2. 全局注册，Vue.component('组件名',组件)
    3. 编写组件标签
        <组件名></组件名>
 -->
<body>
    <div id="root">
        <!-- 第三步：编写组件标签 -->
        <hello></hello>
        <hr>
        <school></school>
        <hr>
        <student></student>
    </div>
    <div id="root2">
        <hello></hello>
    </div>
</body>

<script>
    // 第一步：创建学校组件
    const school=Vue.extend({
        template:`
        <div>
            <h2>学校名称：{{name}}</h2>
            <h2>学校地址：{{address}}</h2>
        </div>
        `,
        data(){
            return {
                name:'苏州中学',
                address:'苏州市'
            }
        }
    })
    //  第一步：创建学生组件
    const student=Vue.extend({
        template:`
        <div>
            <h2>学生姓名：{{name}}</h2>
            <h2>学生年龄：{{age}}</h2>
        </div>
        `,
        data(){
            return {
                name:'wxm',
                age:'25'
            }
        }
    })

    // 第一步：创建hello组件
    const hello=Vue.extend({
        template:`
        <div>
            <h2>你好啊！{{name}}</h2>
        </div>
        `,
        data(){
            return {
                name:'Tom'
            }
        }
    })

    // 第二步：注册组件（全局注册）
    Vue.component('hello',hello)

    const vm = new Vue({
        el: '#root',
        // 第二步：注册组件（局部注册）
        components:{
            // school:school,
            // student:student,
            school,
            student,
        }
    })
    new Vue({
        el:'#root2'
    })
</script>
</html>

```

###### 2.几个注意点

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>非单文件组件</title>
    <script src="../js/vue.js"></script>
    <style>
    </style>
</head>
<!-- 
    几个注意点：
        1. 关于组件名：
            一个单词组成：
                1.（首字母小写）：school
                2.（首字母大写）：School
            多个单词组成
                1.（kebab-case命名）：my-school
                2.（CameCase命名）：MySchool（需要脚手架支持）
            备注：
                1. 组件名尽可能回避HTML中已有的元素名称，例如h1、H2均不行
                2. 可以使用name配置项指定组件在开发者工具中呈现的名称
        2. 关于组件标签
            1. <school></school>
            2. <school/>
            备注：不用脚手架时，<school/>会导致后续组件不能渲染
        3. 一个简写方式：
            const school=Vue.extend(options)可简写为：const school=options
 -->
<body>
    <div id="root">
        <school></school>
        <school/>
    </div>
</body>

<script>
    const school=Vue.extend({
        name:'xuexiao',
        template:`
        <div>
            <h2>学校名称：{{name}}</h2>
            <h2>学校地址：{{address}}</h2>
        </div>
        `,
        data(){
            return {
                name:'苏州中学',
                address:'苏州市'
            }
        }
    })
    const vm = new Vue({
        el: '#root',
        components:{
            school,
        }
    })
</script>
</html>

```

###### 3.组件的嵌套

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>非单文件组件</title>
    <script src="../js/vue.js"></script>
    <style>
    </style>
</head>
<!-- 
 -->
<body>
    <div id="root">
    </div>
</body>

<script>
    //  创建学生组件
    const student=Vue.extend({
        template:`
        <div>
            <h2>学生姓名：{{name}}</h2>
            <h2>学生年龄：{{age}}</h2>
        </div>
        `,
        data(){
            return {
                name:'wxm',
                age:'25'
            }
        }
    })
    // 创建学校组件
    const school=Vue.extend({
        name:'xuexiao',
        template:`
        <div>
            <h2>学校名称：{{name}}</h2>
            <h2>学校地址：{{address}}</h2>
            <student></student>
        </div>
        `,
        data(){
            return {
                name:'苏州中学',
                address:'苏州市'
            }
        },
        components:{
            student
        }
        
    })
    
    // 创建hello组件
    const hello=Vue.extend({
        template:`
        <div>
            <h2>你好啊！{{name}}</h2>
        </div>
        `,
        data(){
            return {
                name:'Tom'
            }
        }
    })
    // 创建app组件
    const app=Vue.extend({
        template:`
        <div>
            <school></school>
            <hello></hello>
        </div>
        `,
        components:{
            school,
            hello,
        }
    })
    const vm = new Vue({
        template:'<app></app>',
        el: '#root',
        components:{
            app,
        }
    })
</script>
</html>

```

###### 4.VueComponent

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>非单文件组件</title>
    <script src="../js/vue.js"></script>
    <style>
    </style>
</head>
<!-- 
    关于VueComponent：
        1. school组件本质上是一个名为VueComponent的构造函数，且不是程序员定义的，是Vue.extend生成的
        2. 我们只需要写<school></school>或者<school/>，Vue解析时会帮我们创建school组件的实例对象，
           即Vue帮我们执行：new VueComponent(options)。
        3. 特别注意：每次调用Vue.extend，返回的都是一个全新的VueComponent
        4. 关于this指向：
            1. 组件配置中：
                data函数、methods中的函数、watch中的函数、computed中的函数 它们的this指向均是【VueComponent实例对象】
            2. new Vue()配置中：
                data函数、methods中的函数、watch中的函数、computed中的函数 它们的this指向均是【Vue实例对象】
        5. VueComponent实例对象，以后简称vc（也可称之为组件实例对象）
            Vue的实例对象，以后简称vm
 -->
<body>
    <div id="root">
        <school></school>
    </div>
</body>

<script>
    const school=Vue.extend({
        template:`
        <div>
            <h2>学校名称：{{name}}</h2>
            <h2>学校地址：{{address}}</h2>
        </div>
        `,
        data(){
            return {
                name:'苏州中学',
                address:'苏州市'
            }
        }
    })
    console.log(school)
    const vm = new Vue({
        el: '#root',
        components:{
            school,
        }
    })
</script>
</html>

```

###### 5.一个重要的内置关系

![image-20230130103537032](C:\Users\xiaom\AppData\Roaming\Typora\typora-user-images\image-20230130103537032.png)

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>非单文件组件</title>
    <script src="../js/vue.js"></script>
    <style>
    </style>
</head>
<!-- 
    1. 一个重要的内置关系：VueComponent.prototype.__proto__===Vue.prototype
    2. 为什么要有这个关系：让组件实例对象（vc）可以访问到Vue原型上的属性、方法。
 -->
<body>
    <div id="root">
        <school></school>
    </div>
</body>

<script>
    Vue.prototype.x=99
    const school=Vue.extend({
        template:`
        <div>
            <h2>学校名称：{{name}}</h2>
            <h2>学校地址：{{address}}</h2>
            <button @click="showx">点我提示x</button>
        </div>
        `,
        data(){
            return {
                name:'苏州中学',
                address:'苏州市'
            }
        },
        methods: {
            showx(){
                alert(this.x)
            }
        },
    })
    new Vue({
        el:'#root',
        components:{
            school
        }
    })
    // 定义一个构造函数
    /* function Demo(){
        this.a=1
        this.b=1
    }
    // 创建一个Demo的实例对象
    const d=new Demo()
    console.log(Demo.prototype)  // 显示原型属性

    console.log(d.__proto__)     // 隐式原型属性
    console.log(d)

    Demo.prototype.x=99
    console.log(d) */


</script>
</html>

```

##### 19.单文件组件

###### App.vue

```vue
<template>
    <div>
        <School></School>
        <Student></Student>
    </div>
  
</template>

<script>
    // 引入组件
    import School from './School.vue';
    import Student from './Student.vue';
    export default {
        name:'App',
        components:{
            School,
            Student,
        }
    }
</script>

<style>

</style>
```

###### index.html

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title>练习一下单文件组件的语法</title>
    </head>
    <body>
        <div id="root">
            <App></App>
        </div>
        <script type="text/javascript" src="../js/vue.js"></script>
        <script type="text/javascript" src="./main.js"></script>
    </body>
</html>
```

###### main.js

```js
import App from './APP.vue'

new Vue({
    el:'#root',
    components:{App}
})
```

###### School.vue

```vue
<template>
     <!-- 组件的结构 -->
    <div class="demo">
        <h2>学校名称：{{ name }}</h2>
        <h2>学校地址：{{ address }}</h2>
        <button @click="showName">点我提示学校名</button>
    </div>
</template>

<script>
    // es6中暴露的三种方式
    export default {
        name:'Scholl',
        data() {
            return {
                name:'苏州中学',
                address:'苏州市'
            }
        },
        methods: {
            showName(){
                alert('this.name')
            }
        },
    }
   

</script>

<style>
    /* 组件的样式 */
    .demo{
        background-color: bisque;
    }
</style>
```

###### Student.vue

```vue
<template>
    <div >
        <h2>学校名称：{{ name }}</h2>
        <h2>学校地址：{{ age  }}</h2>
        <button @click="showName">点我提示学生名</button>
    </div>
</template>

<script>
    export default {
        name:'Student',
        data() {
            return {
                name:'wxm',
                age:20,
            }
        },
        methods: {
            showName(){
                alert('this.name')
            }
        },
    }
</script>

```

##### 20.脚手架

提示：需提前安装好node.js

第一步：全局安装@vue/cli

`npm install -g @vue/cli`

第二步：切换到你要创建项目的目录，然后使用命令创建项目

`vue create xxx`

第三步：启动项目

`npm run server`

如果出现下载缓慢请配置npm淘宝镜像：

`npm config set registry https://registry.npm.taobao.org`

更改vue 中webpack的默认配置

`vue inspect > output.js`
