# 变量、作用域和内存
> 本章将变量，作用域，以及内存的常见问题进行整理
******
## 关于基本类型与引用类型
Javascript中的变量分为两种，即`基本类型`与`引用类型`

`Undefined`、`Null`、`Boolean`、`Number`和`String`这几种类型是基本类型。
`Object`、`Array`、`Date`、`RegExp`、`Function`这几种是引用类型。

基本类型按值访问，可以直接操作保存在变量中的实际值；引用类型是保存在内存中的对象，对对象的操作实际是在对对象的引用进行操作。因此，引用类型是按引用访问的。

对于引用类型，我们可以为其添加属性和方法，也可以改变和删除属性和方法。如下
``` javascript
var person = new Object();
person.name = "Nicholas";
console.log(person.name);       //"Nicholas"
```
而基本类型则不行。如下
``` javascript
var name = "Nicholas";
name.age = 27;
console.log(name.age);      //undefined
```

复制基本类型变量的值到另一个变量的时候，会创建这个值的副本。而引用类型则是复制的指针。如下
``` javascript
var num1 = 5;
var num2 = num1;
num2 = 4;
console.log(num1); //5
var obj1 = new Object();
var obj2 = obj1;
obj1.name = "Nicholas";
console.log(obj2.name);  //"Nicholas"
```

确定一个变量是哪种类型可以只用`typeof`操作符，确定一个变量是是否指定类型可以使用`instanceof`
``` javascript
var s = "Nicholas";
console.log(typeof s);   //string

var person = new Object();
console.log(person instanceof Object);   //true
```


## 关于作用域


## 关于内存


## 小结


