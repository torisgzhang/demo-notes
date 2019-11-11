
``` javascript
/*
apply() 方法调用一个函数, 其具有一个指定的this值，以及作为一个数组（或类似数组的对象）提供的参数
 b.apply(a,[1,2])
 b.call(a,1,2)
apply和call区别就是call()方法接受的是参数列表，而apply()方法接受的是一个参数数组。
bind()方法创建一个新的函数, 当被调用时，将其this关键字设置为提供的值，在调用新函数时，在任何提供之前提供一个给定的参数序列。
*/

/** this指向问题
 */
// 当元素身上的事件被触发的时候，会执行一个函数，函数中的this执行当前这个元素
// 当函数被调用的时候，看前面是否有点，点前面是谁，this就是谁，没有点，this就是window
// 自执行函数中的this，永远指向window
// 回调函数中的this，一般指向window，但是可以通过thisArg更改this指向
// 构造函数中的this，指向实例；
// 当遇到call、apply、bind的时候，以上规则全失效，他们三个就是用来更改this指向的



/**
 * obj.call(thisObj, name, color)
 * 把obj的this绑定到thisObj上，这时候thisObj具备了（或者说继承了）obj的属性和方法，然后在thisObj的执行环境里面执行obj的属性和方法，
 * 绑定后会立即执行函数
**
1，apply和call 本来就是为了扩展函数的作用域而生的，换句话说就是为了改变this的指向存在的
2，当一个object没有某种方法，但是其他的有，我们可以借助call和apply来用其他对象的方法来做操作，也可以传参数
3，apply和call都是传参之后立即执行  bind和call一样的传参  不同点是传参之后不会立即执行，只会返回一个函数的定义阶段，  在需要的地方调用执行
 * 
 */ 

  let arr1 = [1, 2, 3]
  let arr2 = [4, 5, 6]
  arr1.push.apply(arr1, arr2);
  console.log(arr1)

  function Dog(name, color) {
    this.name = name;
    this.color = color;
    this.test = () => {
      return "Dog对象"
    }
  }
  Dog.prototype.bark = () => {
    return ('wangwang~')
  }
  function Husky(name, color, weight) {
    Dog.call(this, name, color)
    this.weight = weight
  }
  Husky.prototype = new Dog();
  var o = new Husky('张三', "白色", 111);
  console.log(o.bark());


//call继承：子类只继承父类“私有”的属性和方法，不继承公有
function F(){
  this.x = 100;
  this.y = 200;
}
F.prototype.a = '公有属性';
F.prototype.showX = function(){
  return "公有方法"
};
var f1 = new F;
console.dir(f1);
console.dir(f1.a);
console.dir(f1.showX);
function Son(){
  F.call(this);
}
var s1 = new Son;
console.dir(s1);
console.dir(s1.a);
console.dir(s1.showX);

//原型链继承
function F(){
  this.x = 100;
  this.y = 200;
}
F.prototype.a = '公有属性';
F.prototype.showX = function(){
  return "公有方法"
};
var f1 = new F;
console.dir(f1);
console.dir(f1.a);
console.dir(f1.showX);
function Son(){
  
}
Son.prototype = new F();
var s1 = new Son;
console.dir(s1);
console.dir(s1.a);
console.dir(s1.showX);
```