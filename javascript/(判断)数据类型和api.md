#### 数据类型包括：

---
**null、undefined、number、string、boolean、symbol、bigint、object**

注意还有新增的symbol和bigint

##### 1、null

---
typeof null ---> object

判断方法：

``` js
var a = null;
if(!a && typeof a ==="object"){console.log('is null')}
```

##### 2、undefined

---

未声明则使用某变量时会报错undefined。

以下为一些报错和普通例子：

``` js
console.log(a);
//Uncaught ReferenceError: a is not defined

var b;console.log(b.c);
//Uncaught TypeError: Cannot read property 'c' of undefined

var b={};console.log(b.c);//undefined

var d=[];console.log(d[0][0])
//Uncaught TypeError: Cannot read property '0' of undefined

var d=[];console.log(d[0])//undefined
```

**声明后未赋值，则是undefined**

##### 3、number

---
##### （1）infinity

---


```
1/0
//Infinity

-1/0
//-Infinity

1/Infinity
//0

-1/Infinity
//-0

1/-Infinity
//-0
```
##### （2）-0的处理
---
原因：如动画帧这种需要保存符号，用来标记方向。

注意：“-0”字符串可以转化为数字-0，但是数字-0不能转化为字符串“-0”

处理：
- polyfill:

``` js
function isNegZero(n){
  n = Number(n);//字符串转化为数字ok
  return (n===0) && (1/n === -infinity)
  
}
```
- Object.is(a,b)  用来判断（NaN和NaN）以及（-0和0）

``` js
Object.is(NaN,NaN); // true
Object.is(0,-0); // false
//普通比较比较不要用这个，效率不高。
```

**number的api：**
- Number.isInteger()
- Number.isSafeInteger()//最大为Math.pow(2,52)

#### 4、string

---
#### 5、boolean

---
#### 6、symbol

---
#### 7、bigint

---

``` js
var num = 968777777777n; // 必须加“n”
console.log(typeof num) // bigint
```

#### 8、object

---
数组和函数均是对象的子类型

<br><br><br><br>


**不是基本数据类型的NaN**

---
意思为：**执行的运算未成功**

**NaN===NaN** ----->**false**

bug：window.NaN('a') // true  (但是我们希望它只表示运算失败，而不是‘不是一个数字’)

修正：
- Number.NaN('a') // false   √
- polyfill：<br>function NaN(a){return a!==a} <br> // 利用了NaN不等于NaN
- Object.is(a,b) // Object.is(NaN,NaN) ---> true

---
判断方法总结：

![alt](https://uploadfiles.nowcoder.com/images/20220312/167993455_1647051454986/D2B5CA33BD970F64A6301FA75AE2EB22)

注意：Boolean和==的隐式转换规则是不同的
