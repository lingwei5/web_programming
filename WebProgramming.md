# Web Programming
跨域：协议 域名 端口任一不同就是跨域
协议
域名
端口

一个完整的URL通常包括以下部分：
   - **协议（Protocol）**：如`http://`或`https://`
   - **主机名（Hostname）**：如`example.com`
   - **端口（Port）**：可选，如`:8080`
   - **路径（Path）**：如`/api/users`
   - **查询参数（Query Parameters）**：可选，如`?id=123&name=foo`
   - **片段（Fragment）**：可选，如`#section1`（通常用于前端页面锚点，不会发送到服务器）

URL:统一资源定位符，用于定位互联网上的资源，如：http://www.example.com/index.html 俗称网络地址，简称网址
可以是服务器上的一个物理文件、动态生成的内容或者一个API端点(endpoint)

当服务器收到一个请求时，它会根据请求的URL路径和请求方法（GET、POST等）来决定由哪个处理程序（handler）来处理这个请求。这个过程称为路由（routing）。

- 如果URL指向的是静态文件目录中的文件，那么它对应服务器上的具体文件。
- 如果URL指向的是后端定义的路由（常见于RESTful API），那么它对应的是一个由后端程序处理的逻辑端点（endpoint），返回的数据是动态生成的（可能是从数据库中获取，经过计算等）。
- 因此，URL具体对应什么，取决于服务器的配置和后端程序的路由设计。

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

script 定义脚本 src:引入外部js文件 
type:定义脚本类型
传统类型:text/javascript
ES6支持module，script type="module" src="./orbitcontroller.js"
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

# Java
package com.example.demo;//包声明，就是个命名空间，防止命名冲突，包名一般用小写字母，一般约定就是xxx.java的文件路径
import 的原理是编译时解析，导出引用或者地址
注解:本质就是一个接口，继承自java.lang.annotation.Annotation,为Java 类或方法提供额外的元数据机制，类似Qt的moc\dicom的meta等，这些信息可以在编译时、加载时或运行时被读取和处理。注解本身不会直接影响代码逻辑，但可以通过其他工具（如编译器、框架等）来改变程序的行为或生成额外的代码
使用注解时，实际上是使用接口的实例,使用反射机制修饰代码
注解的作用：
​- ​编译检查​​：例如@Override注解用于指示方法覆盖了父类的方法，编译器会检查是否真的覆盖，如果没有则报错。
​- ​生成文档​​：例如@Deprecated表示该方法已过时，在生成文档时会特别标记。
​- ​代码分析​​：通过注解，工具可以在编译时或运行时分析代码，例如生成代码、进行验证等。
​- ​框架配置​​：在框架中广泛使用，例如Spring中的@Controller、@Autowired等，用于配置组件和依赖注入。

元注解:注解的注解
@Retention - 保留策略
@Target - 作用目标
@Documented - 文档收录
@Inherited - 继承特性
@Repeatable - 重复注解

@interface - 定义注解
interface - 定义接口


## spring注解
核心注解：
	@Component: 标记一个类为Spring容器管理的组件（Bean）。它是所有Spring管理的组件的通用注解。
	@Service: 用于标记服务层的组件，是@Component的特例。
	@Repository: 用于标记数据访问层（DAO）组件，同时具有将数据库操作抛出的原生异常转换为Spring的DataAccessException的功能。
	@Controller: 用于标记控制器组件（如Spring MVC控制器）。
	@Autowired: 用于自动装配依赖，可以用在字段、构造器、setter方法上。
	@Qualifier: 当有多个相同类型的Bean时，用于指定具体装配哪一个Bean。
	@Value: 用于注入属性值（从properties文件、环境变量等）。
Spring MVC注解：
	@RequestMapping: 用于映射Web请求（URL）到处理方法。可以指定HTTP方法（GET, POST等）。
	@GetMapping, @PostMapping, @PutMapping, @DeleteMapping, @PatchMapping: 分别对应不同HTTP方法的请求映射。
	@RequestParam: 用于获取请求参数。
	@PathVariable: 用于获取URL模板变量（即路径变量）。
	@RequestBody: 用于将HTTP请求体转换为Java对象（通常用于接收JSON/XML数据）。
	@ResponseBody: 用于将方法返回的对象直接写入HTTP响应体（通常用于返回JSON/XML数据）。
	@RestController: 组合注解，相当于@Controller和@ResponseBody的组合，用于RESTful Web服务。
	@ModelAttribute: 用于绑定请求参数到模型对象，或者用于在方法执行前初始化模型对象。
配置相关注解：
	@Configuration: 标记一个类为配置类，相当于XML配置文件。
	@Bean: 在配置类中声明一个Bean，方法返回的对象将被Spring容器管理。
	@ComponentScan: 用于自动扫描并注册组件（配合@Configuration使用）。
	@PropertySource: 用于加载properties文件到Spring的环境变量中。
	@Import: 用于导入其他配置类。
	@Profile: 用于指定Bean在哪个环境（profile）下被激活。
事务管理注解：
	@Transactional: 用于声明事务（方法或类级别），可以配置事务的传播行为、隔离级别、超时等。
测试相关注解：
	@SpringBootTest: 用于Spring Boot应用的集成测试，会加载完整的应用程序上下文。
	@Test: 标记一个方法为测试方法（JUnit）。
	@MockBean: 在Spring测试中模拟一个Bean。
切面编程（AOP）注解：
	@Aspect: 声明一个切面。
	@Pointcut: 定义切点表达式。
	@Before, @After, @AfterReturning, @AfterThrowing, @Around: 定义通知类型（在切点之前、之后等执行）。
Spring Boot特有注解：
	@SpringBootApplication: 用于主配置类，是@Configuration、@EnableAutoConfiguration和@ComponentScan的组合。
	@EnableAutoConfiguration: 启用Spring Boot的自动配置机制。
条件注解（Conditional）：
	@ConditionalOnClass, @ConditionalOnMissingBean, @ConditionalOnProperty等：根据条件决定是否创建Bean。
异步与调度：
	@Async: 标记方法为异步执行。
	@EnableAsync: 启用异步方法执行功能。
	@Scheduled: 标记方法为定时任务。
	@EnableScheduling: 启用定时任务功能。
安全注解（Spring Security）：
	@EnableWebSecurity: 启用Web安全配置。
	@Secured: 用于方法安全，指定访问该方法的角色列表。
	@PreAuthorize, @PostAuthorize: 方法执行前/后进行权限检查。
验证注解（Bean Validation）：
	@Valid: 用于触发对方法参数的验证（通常与@RequestBody一起使用）。
	@NotBlank, @Email, @Size等: 用于字段验证的约束注解。
缓存注解：
	@Cacheable: 标记方法的结果可缓存。
	@CacheEvict: 标记方法用于清除缓存。
	@CachePut: 更新缓存。
	@EnableCaching: 启用缓存功能。
消息注解（Spring Messaging）：
	@MessageMapping: 用于映射消息（如WebSocket消息）到处理方法。
	@SendTo: 指定处理方法的返回消息发送到哪个目的地。
国际化（i18n）：
	@LocaleResolver: 配置区域解析器。
	@MessageSource: 配置国际化消息源。
其他：
	@Lazy: 延迟初始化Bean。
	@Scope: 指定Bean的作用域（如：prototype, request, session等）。
	@Primary: 当有多个同类型Bean时，标记为首选Bean。


web技术演进

静态网页1991-1995 无js--> 动态网页php95 js95 servelet/jsp97--->web2.0 ajax 2005 jQuery AngularJS--->web3.0 2010 react vue angular--->web4.0 2018 WebAssembly webGPU WebXR

![alt text](php-asp-servlet-jsp.png)
![alt text](asp-asp.net.svg)
![alt text](php到现代框架.svg)
![alt text](<jsp到spring boot.svg>)

![alt text](asp-asp.net.svg)
![alt text](php到现代框架.svg)
![alt text](<jsp到spring boot.svg>)

![alt text](技术演进规律.png)
