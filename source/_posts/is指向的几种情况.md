title: this指向的几种情况
author: 郭峰
tags:
  - 前端基础
categories:
  - js
date: 2020-01-04 14:30:00
---
* 哪个对象调用函数，函数里面的this指向哪个对象。

分几种情况谈论下
## 普通函数调用
* 这个情况没特殊意外，就是指向全局对象-window。

```
var username='cn'
function fn(){
    alert(this.username);//undefined
}
fn();

------------------------------------------------------------------
var username='cn'
function fn(){
    alert(this.username);//cn
}
```
<!--more-->
## 对象函数调用

* 哪个函数调用，this指向哪里

```
window.b=2222
let obj={
    a:111,
    fn:function(){
        alert(this.a);//111
        alert(this.b);//undefined
    }
}
obj.fn();
```
下面这种情况虽然obj1.fn是从obj2.fn赋值而来，但是调用函数的是obj1，所以this指向obj1
```    
let obj1={
        a:222
    };
    let obj2={
        a:111,
        fn:function(){
            alert(this.a);
        }
    }
    obj1.fn=obj2.fn;
    obj1.fn();//222
```
## 构造函数调用

```
let TestClass=function(){
    this.name='111';
}
let subClass=new TestClass();
subClass.name='cn';
console.log(subClass.name);//cn
let subClass1=new TestClass();
console.log(subClass1.name)//111
```

## apply和call调用
apply和call简单来说就是会改变传入函数的this。

```
    let obj1={
        a:222
    };
    let obj2={
        a:111,
        fn:function(){
            alert(this.a);
        }
    }
    obj2.fn.call(obj1);111
```
* call 和 apply 的作用，完全一样，唯一的区别就是在参数上面。
* call 接收的参数不固定，第一个参数是函数体内 this 的指向，第二个参数以下是依次传入的参数。
* napply接收两个参数，第一个参数也是函数体内 this 的指向。第二个参数是一个集合对象（数组或者类数组）

```
    let fn=function(a,b,c){
    console.log(a,b,c);
    }
    let arr=[1,2,3];
    fn.call(window, arr) // [1,2,3]
    fn.apply // 1, 2, 3
```

call 和 apply 两个主要用途就是

1.改变 this 的指向（把 this 从 obj2 指向到 obj1 ）

2.方法借用（ obj1 没有 fn ，只是借用 obj2 方法）

## 箭头函数调用

箭头函数里面，没有 this ，箭头函数里面的 this 是继承外面的环境。

```
let obj={
    a:222,
    fn:function(){    
        setTimeout(function(){console.log(this.a)})
    }
};
obj.fn();//undefined
```

虽然 fn() 里面的 this 是指向 obj ，但是，传给 setTimeout 的是普通函数， this 指向是 window ， window 下面没有 a ，所以这里输出 undefined。

```
    let obj={
        a:222,
        fn:function(){    
            setTimeout(()=>{console.log(this.a)});
        }
    };
    obj.fn();//222
```
输出 222 是因为，传给 setTimeout 的是箭头函数，然后箭头函数里面没有 this ，所以要向上层作用域查找，在这个例子上， setTimeout 的上层作用域是 fn。而 fn 里面的 this 指向 obj ，所以 setTimeout 里面的箭头函数的 this ，指向 obj 。所以输出 222 。