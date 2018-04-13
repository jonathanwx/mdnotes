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


## 关于执行环境与作用域
每个函数都有自己的执行环境。当执行流进入一个函数时，函数的环境就会被推入一个环境栈中。而在函数执行之后，栈将其环境弹出，把控制权返回给之前的执行环境。
当代码在一个环境中执行时，会创建变量对象的作用域链。作用域链能够保证执行环境对变量和函数的有序访问。
标识符的解析是沿着作用域链一级一级搜索的过程。作用域连的最前端是当前执行的代码所在的环境的变量对象，如果环境时函数，则将其活动对象作为变量对象，活动对象最开始只包含`arguments`对象。作用域链的下一个变量则是当前环境的外部环境，如此直到全局执行环境，即`window`。全局环境始终都是作用域链中的最后一个对象。

``` javascript
var color = "blue";
function changeColor(){
    if (color === "blue"){
        color = "red";
    } else {
        color = "blue";
    }
}
changeColor();
console.log("Color is now " + color); //Color is now red
```
如上所示代码中，`changeColor()`的只作用域链包含两个对象，即自身变量对象（包含了`arguments`）和全局环境变量。所以函数内部能够访问到`color`。

下边这个例子阐述了全局环境与局部环境中变量访问权限。
``` javascript
var color = "blue";
// 这里只能访问color
function changeColor(){
    // 这里可以访问color和anotherColor，但不能访问tempColor
    var anotherColor = "red";
    function swapColors(){
        // 这里可以访问color、anotherColor和tempColor
        var tempColor = anotherColor;
        anotherColor = color;
        color = tempColor;        
    }    
    swapColors();
}
changeColor();
```

javascript中没有块级作用域的说法，不像类C语言中花括号中的代码都有自己的执行环境

1. 执行环境有全局执行环境（也称为全局环境）和函数执行环境之分
1. 每次进入一个新执行环境，都会创建一个用于搜索变量和函数的作用域链
1. 函数的局部环境不仅有权访问函数作用域中的变量，而且有权访问其包含（父）环境，乃至全局环境
1. 全局环境只能访问在全局环境中定义的变量和函数，而不能直接访问局部环境中的任何数据
1. 变量的执行环境有助于确定应该何时释放内存。


## 关于内存
