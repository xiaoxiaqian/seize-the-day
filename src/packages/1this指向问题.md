## 函数式调用

_当一个函数并非一个对象的属性时，那么它就是被当作函数来调用的。再此种模式下，this 被绑定为全局对象，在浏览器环境下就是 window 对象_
```
function fn(){
    var a = 'hello'
    console.log(this.a)    
    console.log(this)  
 }
 fn()  // undefined window 
```
## 方法调用模式
  _当函数被保存为一个对象的属性时，它就可以被称为这个对象的方法。当一个方法被调用时，this被绑定到这个对象上。如果调用表达式包含一个提取属性的动作（. 或 []）那么它被称为方法调用_
  ```
    var o = {
        name:'hello',
        sayName:function(){
            console.log(this.name)
        }
    }
    o.sayName()
    // 打印 hello  这里的this指向 o，因为sayName函数是通过 o.sayName() 执行的
  ```
  ```
    var o = {
        name:'hello',
        b:{
            fn:function(){
                console.log(this.name)
                console.log(this)
            }
        }
    }
    o.b.fn()
    // 打印 undefined 和 b 对象，因为是o.b调用的这个函数，所以this 指向 b
  ```
  ```
  var name = '我是最外层的name'
    var o = {
      name: 'hello',
      b: {
        name: 'world',
        fn: function () {
          console.log(this.name)
          console.log(this)
        }
      }
    }
    var b = o.b.fn
    b()
    // 打印  我是最外层的name window 
    // b 是全局变量 在全局环境下执行，this指向window 
  ```
  ## 构造函数调用模式
  _如果在一个函数前面加上new关键字来调用，那么就会创建一个连接到该函数prototype成员的新对象，同时this会被绑定到这个新对象上，这种情况下，这个函数就被叫做这个新对象的构造函数_
  ```
  function fn(){
      console.log(this)
  }
  var a = new fn()
  a()  

  在构造函数，new出一个对象时，this指向这个构造函数，new关键字会改变this的指向
  ```
  ```
  function fn(){
      this.name = 'hello'
  }
  var f = new fn()
  console.log(f.name)  // 打印 hello
-------------------------------------------------------
function fn2(){
    this.name = 'hello2'
    return {}
}
var f2 = new fn2()
console.log(f2.name)  //打印 undefined
// 当用new关键字，返回的是一个对象，this指向的就是那个返回的对象；如果返回的不是对象，this还是指向函数的实例，虽然null属于对象，但是返回null依然指向函数实例,例子：
----------------------------------------------------------------
 function fn3() {
      this.name = 'hello3'
      return null
    }
    var f3 = new fn3()
    console.log(f3)  // 打印 { name:'hello3'}
    console.log(f3.name)  //返回null this还是指向实例 打印 hello3
    ----------------------------------------------------------
    fn3 return 1  不是对象，this指向实例 打印  hello3
    fn3 return 函数 是一个对象this指向这个返回的对象 打印 undefined
    fn3 return undefined 不是一个对象 打印 hello3
    fn3 return [] 是一个对象 打印 undefined
  ```
## apply 和 call 调用
_js中函数也是对象，所有函数对象都有两个方法apply和call，这两个方法可以让我们构建一个参数数组传递给函数调用也允许我们改变this的值 _
```
  var name = 'window'
  var o = {
    name:'obj'
  }
  function sayName(){
    console.log(this.name)
  }
  sayName()   //window
  sayName.apply(o) // obj
  sayName.call(o) // obj
  sayName.apply() // window
  sayName.call()  // window
```

# 总结 
- 在全局范围内，this指向全局对象(浏览器环境下指向window)
- 对象函数调用时，谁调用this指向谁
- 全局函数调用时，应该是指向全局函数的对象
- 使用new关键字实例化对象时 this 指向新创建的对象
- 当用 call apply 上下文调用的时候，指向传的第一个参数