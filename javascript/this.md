（以下不考虑严格模式）



# this

## 1、普通函数的this：
---
 **默认绑定全局对象** 或者 **指向调用者** 
 

> 对象属性获取this的原则：
It’s trying to get the [[Base]] property of the reference (which is e.g. refObj, when applied to refObj.func; or foo.bar when applied to foo.bar.baz).

##### 手动绑定this

名称 | 缩写
:---: | :---:
call、apply | .call(obj);  .apply(obj); 
bind | 调用f.bind(someObject)会创建一个与f具有相同函数体和作用域的函数 ,this将永久地被绑定到了bind的第一个参数

``` js
function f(){
  return this.a;
}
var h = f.bind({a:'yoo'}); // bind this永久生效，传值还可以正常传递

console.log(h());
```
## 2、箭头函数的this：
-----

名称 | 缩写
:---: | :---:
非对象属性 | 该箭头函数在定义时，所处执行文中 迭代向上寻找的最近上层环境的this
对象的属性 | globalThis

> 词法作用域只由函数被声明时所处的位置决定


> When calling a function as a property of an object, it is called with the this binding set to globalThis.

``` js
var c=6
function refObj(){
    let c=9;
   let a= {
    e:{
        d:()=>this.c,
    },
  }
    console.log(a.e.d())
}
refObj() //6
```

https://stackoverflow.com/questions/3127429/how-does-the-this-keyword-work-and-when-should-it-be-used





------
### 以下为旧版记录

1、
``` js
var globalObject = this;
var foo = (() => this);
console.log(foo() === globalObject); // true

```
2、

``` js
var obj = {
  bar: function() {
    var x = (() => this);
    return x;
  }
};

// 作为 obj 对象的一个方法来调用 bar，把它的 this 绑定到 obj。
// 将返回的函数的引用赋值给 fn。
var fn = obj.bar();
console.log(fn() === obj); // true

// 只是引用 obj 的方法，
var fn2 = obj.bar;
console.log(fn2()() == window); // true
```


``` js
c=1;
let a={b:function(){return ()=>this.c},c:3}
a.b()()//3

c=1;
let a={d:{b:function(){return ()=>this.c},c:3},c:5}
a.d.b()()//3

c=1;
let a={d:{b: ()=>this.c,c:3},c:5}
a.d.b()//1

c=1;
let a={f:{d:{b: ()=>this.c,c:3},c:5},c:9}
a.f.d.b()//1
```
构造函数的this不遵循对象的this

``` js
var a=999;
const refObj = {
    e:{
        c:function(){
            console.log(this.k);
            console.log(this);
        },
        k:this.a
    },
    b:2
  };
 refObj.e.c()
// 999
// {k: 999, c: ƒ}

```

![alt](https://uploadfiles.nowcoder.com/images/20230626/167993455_1687759730756/D2B5CA33BD970F64A6301FA75AE2EB22)

**词法作用域**

---

**作用域链**

---

在编译阶段，词法作用域就已确立（这是建立在无eval和with等动态添加代码的情况下），此时确立了用于函数调用时的变量标识。故而函数寻找变量是在作用域链中寻找，而不是根据调用时的嵌套关系，与调用无关，与定义有关。如下代码：

``` js
        var b = 1;
        function aaa() {
            var a = 2;
            console.log(c)//Uncaught ReferenceError: c is not defined
        }
        function bbb() {
            var c = 3;
            console.log("这里可以访问到b,b为", b)//这里可以访问到b,b为 1
            aaa();
            //这里实际在bbb这个词法环境中并不能找到aaa这个函数
            //而是到他的作用域链中寻找，于是找到了外层环境的window
        }
        bbb()
```
即使调用是嵌套的，也不能在aaa中获取到bbb的变量。明显可以看出作用域不是在调用时确定的，其实是在编译阶段，上下文对象就已经确立了，在函数调用时，将调用上下文，其中包含了作用域链。

``` js
 var b = 1;
function bbb() {
   function aaa() {
      var a = 2;
      console.log(c)//3
   }
    var c = 3;
    console.log("这里可以访问到b,b为", b)//这里可以访问到b,b为 1
    aaa();
}
bbb()
```


---

**执行上下文**

---
在**编译阶段执行上下文就已确立**，包括包含的作用域链。

执行上下文上下文包含了：**变量对象、this以及作用域链**

进入执行上下文时，**VO的初始化**过程具体如下：

- 函数的**形参**（当进入函数执行上下文时） 变量对象的一个属性，其属性名就是形参的名字，其值就是实参的值；对于没有传递的参数，其值为undefined

- 函数**声明**（FunctionDeclaration, FD） 变量对象的一个属性，其属性名和值都是函数对象创建出来的；如果变量对象已经包含了相同名字的属性，则替换它的值

- 变量**声明**（var，VariableDeclaration） 变量对象的一个属性，其属性名即为变量名，其值为undefined;如果变量名和已经声明的函数名或者函数的参数名相同，则不会影响已经存在的属性。

当执行到某一函数时，将该**执行上下文加入调用栈**，将**激活活动对象**（AO）。
AO是在进入函数的执行上下文时创建的，并为该对象初始化一个**arguments属性**，该属性的值为Arguments对象，（变量对象+arguments）。

推荐：https://leohxj.gitbooks.io/front-end-database/content/javascript-advance/scope-chain.html