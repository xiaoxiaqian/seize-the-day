## 函数式调用

_当一个函数并非一个对象的属性时，那么它就是被当作函数来调用的。再此种模式下，this 被绑定为全局对象，在浏览器环境下就是 window 对象_
```
function a(){
    var a = 'hello'
    console.log(this.a)    // undefined
    console.log(this)     // window
 }
```
