<!--
$theme: gaia
template: gaia
-->


Node.js深入理解
异步回调的注意点<p style="text-align:right;font-size:28px;margin-right:50px;color:#cFc;">:star: by calidion</p>
===
---
必须要有回调函数
===

```
asyncFunc(param1, param2, () => {
});

asyncFunc(param1, param2, funciton () {
});

asyncFunc(param1, param2, callback);

```
---
回调函数第一个参数必须是error
==

```
asyncFunc(param1, param2, (error) => {
});

asyncFunc(param1, param2, funciton (error) {
});

```
当error为false/null/undefined的时候，表示执行正确
```
if (error) {
// 你的代码
return;
}
```
---
注意回调函数后面的执行
===
1. 通常回调后，原来的函数的执行都必须放入到回调函数内
2. 特别是依赖回调执行后生成的数据的情况

同步执行代码：
```
function () {
Func1(a, b)
Func2(c)
Func3(d)
}
```

---

异步执行代码：
```
function (cb) {
asyncFunc1(a, b, (c) => {
  asyncFunc2((d) => {
     c = xxx
     asyncFunc3(c, () => {
       cb()
     });
  });
});
}
```
