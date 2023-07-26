写在前面：这本书写的很实在，没有基础的很适合，就是可能某些地方不太懂，但没关系，学习本来就不会一下子全懂的。

### instanceof
一个对象是否是特定构造函数的实例
（instanceof只适用于构造函数创建返回的复杂对象和实例，返回原始值的则不行，如原始值string、number、boolean）


### 原始构造函数有：

Number、String、Boolean、Object、Array、Function、Date、RegExp、Error

### 中括号表示法

尤其在无效标识符时，可使用中括号赋值和获取，因为是无效标识符，只能使用中括号进行赋值和获取。如：myobject["123"]

对应直接赋值时，用中括号获取：

``` js
a={' b':1} // {" b": 1}
a[' b'] // 1
```

### for in

- 只能遍历可枚举属性，比如构造函数就遍历不出来，可用propertyIsEnumerable()判断。
- 还会遍历原型链
- 顺序不定

### 浏览器对象

- 宿主对象
- 原生对象

### 编写自用js库

如果有某些常用方法，可以封装起来便于使用。

### Object

new Object() 传不同参进去，可以**创建其他拥有构造函数的原生对象**

如：
``` js
a = new Object('foo') //String {"foo"}
```
### 函数
#### 函数是一等公民

书中有强调这一点，个人理解为以下原因：
1. JavaScript中对象很多（但原始值不是对象），而函数为对象就有了它强大的基础，当然这也体现在原型链最底是Object.prototype。
2. 函数可以当作普通的变量随意存储，可以返回函数、传递函数
3. 函数也可以拥有像对象一样的属性

总结：最需要注意就就是，它可以作为参数传递，还可以作为返回值返回，这给我们留下了发挥空间。

#### arguments
##### arguments.length 调用时传入的参数长度
- 已弃用,但我在控制台依然能用
##### arguments.callee 对当前函数的自我引用
- 在递归时可以进行递归自我回调

##### arguments.callee.length 函数所需参数数量
-   直接用函数的名字.length也行
``` js
a = function(){console.log(arguments.callee.length}
//a = function(){console.log(a.length)}
```
##### 重定义函数参数
- 这个大概是与es6新增的函数默认值相关吧。
- 他的做法就是在函数内给参数了一个初始值，也可以通过arguments下标进行参数初始值赋值。

#### call、apply
- 第一个参数指定了this，也就是在使用this时，按第一个参数的指向
- 第二个参数指定了arguments，这个就是arguments下标获取值。

#### 函数声明提升
- 这个提升连语句都提升了，提前加入执行堆栈（上下文）里了。也就可以在声明之前调用该函数。
- 但表达式函数声明则不同哦。

#### 函数是可以调用自身的

``` js
function a(num){
  console.log(num)
  if(num===0){return false}
  else{
    a(--num)
  } 
}
```
和arguments.callee()一样的
<br>

---
### 以下是知道了也无所谓的一些知识

#### Function

1、构造函数式定义

``` js
a = new Function('a,b','return a+b') // new可省略，一样的
```

这样不建议的原因是因为在解析时使用了eval（eval有很多坏处，私下了解）

2、返回值

不显示声明返回值时，默认隐式返回值为undefined
