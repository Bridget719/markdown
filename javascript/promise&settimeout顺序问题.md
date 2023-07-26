
``` js
var p1 = new Promise(function(resolve, reject){
    resolve(1);
})
setTimeout(function(){
  console.log("will be executed at the top of the next Event Loop");
},0)
p1.then(function(value){
  console.log("p1 fulfilled");
})
setTimeout(function(){
  console.log("will be executed at the bottom of the next Event Loop");
},0)

```

由于then在此代码中会先于setTimeout执行，于是就有了then和setTimeout的时序问题。和所写代码的目的不太一致，因为then是微任务。

promise和setTimeout共同使用时，要将setTimeout封装起来，就能避免类似问题。