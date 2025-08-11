# Web Programming
跨域：协议 域名 端口任一不同就是跨域
协议
域名
端口

/:根目录 localhost:8080 web应用的启动路径作为服务的根目录
./:当前目录
../:上一级目录
文件相对路径:相对于web应用的路径，
html  js
url:统一资源定位符 带.html会直接访问html文件，不带.html会识别为路径，触发重定(向访问index.html)或404
# HTML
静态资源
动态资源:js node.js等生成
html转义字符 &，可以用来在网页展示html tag标签

各种tag标签的用途 及属性

<script/>定义脚本 src:引入外部js文件 
type:定义脚本类型
传统类型:text/javascript
ES6支持module，<script type="module" src="./orbitcontroller.js">
type="importmap"
特点:
1. 模块作用域 封装性
2. 支持import export

# Javascript
对象 函数 类 方法
## 函数：
函数可以通过声明定义，也可以是一个表达式,";"用来分割可执行的JavaScript语句
1. 函数声明 **function functionName(parameters){statements}**无";"在使用的地方进行调用**functionName(parameters);**
2. 函数表达式定义一个函数 var x = function (a, b) {return a * b}; var z = x(4, 3); 实际是一个匿名函数，通过变量名调用
3. Function构造函数
4. 函数提升:函数声明会被提升到作用域的顶部，函数表达式不会被提升
5. 自调用函数:函数表达式可以自调用,即自动调用，(function(){})()函数表达式后面紧跟()就会自动调用,声明的函数无法自调用,实际是匿名自我调用函数
6. js函数是一个对象,有属性和方法,如arguments.length,arguments.callee,arguments.callee.caller
7. 箭头函数表达式:ES6支持箭头函数表达式，语法为：var x = (parameters) => {statements}; 如果只有一个参数，可以省略括号，如果只有一条语句，可以省略花括号和return关键字，如：var x = (a, b) => a * b;

## 对象：
对象是变量的容器，是键值对的容器，对象是属性的无序集合，属性是键值对，键是字符串，值可以是任意类型，如：var person = {firstName:"John", lastName:"Doe", age:50, eyeColor:"blue"};
1. 对象的属性可以通过点符号或方括号来访问，如：person.firstName或person["firstName"]
2. 对象的属性可以通过点符号或方括号来修改，如：person.firstName = "Mike"或person["firstName"] = "Mike";
3. 对象方法是包含函数定义的属性，如：var person = {firstName:"John", lastName:"Doe", age:50, eyeColor:"blue", fullName: function() {return this.firstName + " " + this.lastName;}}
4. 方法的访问方式与属性相同，如：person.fullName()或person["fullName"]();person.fullName打印函数体，person.fullName()打印函数返回值

## 类：
类是对象的蓝图，类可以定义属性和方法，如：class Car { constructor(brand) { this.carname = brand; } }
1. 类的构造函数用于创建对象，构造函数的参数是对象的属性，构造函数的this关键字用于引用对象的属性，如：this.carname = brand;


## prototype
每个JavaScript对象(null除外)在创建时都会关联另一个对象，这个对象就是我们所说的原型，每个对象都会从原型继承属性和方法，原型链是JavaScript中实现继承的一种方式，原型链的顶端是Object.prototype，Object.prototype没有原型，原型链的终点是null。

## import export
ES6支持模块化，模块是自包含的代码单元，可以导入和导出，模块可以包含变量、函数、类等，模块的导入和导出使用import和export关键字，如：export {myFunction, myVariable};import {myFunction, myVariable} from './myModule.js';

导出包含命名导出和默认导出
命名导出需要使用{}包裹，并且名字完全一致，可以as重命名
一个模块只能有一个默认导出export default ，默认导出可以是任何类型的值，如：export default function() {console.log('Hello, world!');}, 导入时可以任意命名 本质是import {default as myFunction} from './myModule.js';
一个文件/脚本就是一个模块

$变量:
1. jQuery中是jQuery的别名，存储jQuery对象，可以通过$访问jQuery对象的方法和属性，如：$(document).ready(function(){});
2. 在Node.js中是全局变量，存储当前模块的上下文对象，可以访问当前模块的属性和方法，如：console.log(module.filename);
3. 在现代前端框架中，如React、Vue等，$变量通常用于存储框架的实例，可以通过$访问框架的方法和属性，如：ReactDOM.render(<App />, document.getElementById('root'));

# CSS
![alt text](Box模型.png)
不同部分的说明：
- Margin(外边距) - 清除边框外的区域，外边距是透明的。
- Border(边框) - 围绕在内边距和内容外的边框。
- Padding(内边距) - 清除内容周围的区域，内边距是透明的。
- Content(内容) - 盒子的内容，显示文本和图像。

插入样式表的三种方式：
1. 外部样式表：在HTML文件中通过<link>标签引入外部CSS文件，如：<link rel="stylesheet" type="text/css" href="style.css">
2. 内部样式表：在HTML文件中使用<style>标签定义CSS样式，如：<style type="text/css">body {background-color: yellow;}</style>
3. 内联样式表：在HTML元素的style属性中定义CSS样式，如：<p style="color: red;">This is a paragraph.</p>

![alt text](CSS基本语法.png)
https://www.runoob.com/cssref/css-selectors.html
1. id选择器:#id {color: red;} id选择器用于选择具有特定id属性的元素，id属性是唯一的，id选择器可以用于任何元素。
2. class选择器:.class {color: red;} class选择器用于选择具有特定class属性的元素，class属性可以用于任何元素。
3. 元素选择器:element {color: red;} 元素选择器用于选择具有特定元素的元素，如：p {color: red;} 选择所有的段落元素。
4. 属性选择器:[attribute=value] {color: red;} 属性选择器用于选择具有特定属性的元素，如：[title=hello] {color: red;} 选择所有具有title属性且值为hello的元素。可以有各种表达式
5. 后代选择器:element element {color: red;} 后代选择器用于选择具有特定元素的后代元素，如：div p {color: red;} 选择所有div元素中的段落元素(不论嵌套了几层)。
6. 子元素选择器:element > element {color: red;} 子元素选择器用于选择具有特定元素的子元素，如：div > p {color: red;} 选择所有div元素的直接子元素(只能是第一层子元素)。
7. 相邻兄弟选择器:element + element {color: red;} 相邻兄弟选择器用于选择具有特定元素的相邻兄弟元素，如：h1 + p {color: red;} 选择所有h1元素后面的第一个段落元素。
8. 通用兄弟选择器:element ~ element {color: red;} 通用兄弟选择器用于选择具有特定元素的通用兄弟元素，如：h1 ~ p {color: red;} 选择所有h1元素后面的所有段落元素。
9. 伪类选择器:element:pseudo-class {color: red;} 伪类选择器用于选择具有特定状态的元素，如：a:hover {color: red;} 选择所有鼠标悬停的链接元素。
10. 伪元素选择器:element:pseudo-element {color: red;} 伪元素选择器用于选择具有特定位置的元素，如：p:first-line {color: red;} 选择所有段落的第一行。
11. 组合选择器:element1, element2 {color: red;} 组合选择器用于选择具有特定元素的元素，如：p, div {color: red;} 选择所有段落和div元素。
12. 



# Three.js
# WebGL