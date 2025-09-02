# 概览
vue是一个渐进式的JavaScript框架，用于构建用户界面和单页应用程序。它使用组件化的方式来构建应用程序，使得代码更加模块化和可维护。
vue项目结构:
	my-vue-app/
	├── node_modules/       # 项目依赖的第三方库
	├── public/             # 静态资源文件夹
	│   ├── index.html      # 应用的 HTML 模板
	│   └── ...             # 其他静态资源（如图片、字体等）
	├── src/                # 项目源代码
	│   ├── assets/         # 静态资源（如图片、字体等）
	│   ├── components/     # 可复用的 Vue 组件
	│   ├── views/          # 页面级组件
	│   ├── App.vue         # 根组件
	│   ├── main.js         # 项目入口文件
	│   ├── router.js       # 路由配置 vue-router
	│   ├── store.js        # Vuex/pinia 状态管理配置
	│   └── ...             # 其他配置和资源
	├── package.json        # 项目配置和依赖管理 npm rum执行的脚本就在这里定义
	├── package-lock.json   # 依赖的精确版本锁定文件
	└── README.md           # 项目说明文档

index.html->main.js->App.vue->components

浏览器默认加载index.html-->引入main.js，main.js引入App.vue作为根组件创建vue应用实例并挂载到html的tag，App.vue引入components构建页面

Vue 应用的 HTML 模板文件是 index.html，它引入了 main.js 文件。main.js 文件引入了 App.vue 文件，并使用 Vue 的 createApp 函数创建了一个 Vue 应用实例，并将 App.vue 组件挂载到 HTML 的 <div id="app"> 元素上。App.vue 文件引入了 components 文件夹中的组件，并使用这些组件构建了页面的结构。


Vue组件:
1. Single-File Components单文件组件SFC .vue文件,Vue 的单文件组件会将一个组件的逻辑 (JavaScript)，模板 (HTML) 和样式 (CSS) 封装在同一个文件里
2. template 使用html vue语法构建UI 虚拟DOM
3. script 使用js语法构建逻辑 export default 导出组件选项 
4. style 使用css语法构建样式 scoped表示样式只作用于当前组件

## 底层原理
Vue项目的运行流程:
1. npm run dev/serve启动项目 or yarn serve,启动开发服务器
2. 构建生成环境代码 npm run build or yarn build
3. 代码格式化 npm run lint or yarn lint

从高层面的视角看，Vue 组件挂载时会发生如下几件事：

	- 编译：Vue 模板被编译为渲染函数：即用来返回虚拟 DOM 树的函数。这一步骤可以通过构建步骤提前完成，也可以通过使用运行时编译器即时完成。

	- 挂载：运行时渲染器调用渲染函数，遍历返回的虚拟 DOM 树，并基于它创建实际的 DOM 节点。这一步会作为响应式副作用执行，因此它会追踪其中所用到的所有响应式依赖。

	- 更新：当一个依赖发生变化后，副作用会重新运行，这时候会创建一个更新后的虚拟 DOM 树。运行时渲染器遍历这棵新树，将它与旧树进行比较，然后将必要的更新应用到真实 DOM 上去。

![alt text](vue渲染管线.png)

VUE文件应该是被编译构建成js css 在底层机制中，Vue会将模板编译成高度优化的 JavaScript 代码
__sfc__ 是 Vue 的一个内部变量，用于标识一个文件是一个单文件组件 (Single File Component)。在 Vue 的编译器中，当它遇到一个 .vue 文件时，会将其解析为一个单文件组件，并将其编译成 JavaScript 和 CSS 代码。然后，这些代码会被打包成一个 JavaScript 文件，并在浏览器中运行。

function render(_ctx, _cache, $props, $setup, $data, $options) {
  return (_openBlock(), _createElementBlock(_Fragment, null, [
    _createElementVNode("h1", null, _toDisplayString($setup.msg), 1 /* TEXT */),
    _withDirectives(_createElementVNode("input", {
      "onUpdate:modelValue": _cache[0] || (_cache[0] = $event => (($setup.msg) = $event))
    }, null, 512 /* NEED_PATCH */), [
      [_vModelText, $setup.msg]
    ])
  ], 64 /* STABLE_FRAGMENT */))
}
__sfc__.render = render
__sfc__.__file = "src/App.vue"


components()定义或者获取一个全局组件
export default {
	name:xxx,//组件名
	data(){
	},//组件数据,组件内部的私有状态，在组件内部定义、修改、使用，作用域限于组件内，不暴露给父组件，虽然技术上可以
	watch:{
	    
	}
	methods:{
	},
	computed:{
	    
	},
	components:{
	    
	},
	props:['',''] or {title:String, likes:Number}//父组件传递给子组件的属性，是HTML tag attribute的扩展，可以静态或动态绑定

}定义局部组件
   
## vue API风格
1. Options API:通过定义组件的选项对象来配置组件的行为，例如data、methods、computed、mounted等
2. Composition API:通过定义函数来组织组件的逻辑，例如setup函数、reactive、ref等
是对同一个底层系统所提供的两套不同的接口，选项式 API 是在组合式 API 的基础上实现的
vue2 vue3选项式api this.$router === useRouter()

## vue生命周期
beforeCreate:组件实例刚刚被创建，组件的属性和方法还没有被初始化
created:组件实例已经被创建，组件的属性和方法已经被初始化
beforeMount:组件实例刚刚被挂载到DOM上，组件的模板还没有被渲染
mounted:组件实例已经被挂载到DOM上，组件的模板已经被渲染

## 调试
1. 组件调试钩子 onRenderTracked/onRenderTriggered
2. computed属性调试:onTrack/onTrigger
3. watch属性调试:onTrack/onTrigger
4. vue 可以配置vite的自动导入插件 vite/plugins/auto-import.js 生成 auto-imports.d.ts文件,include进jsconfig.json里
5. vite:import.meta vite提供的特殊对象，可以访问env 如import.meta.env.VITE_APP_BASE_URL等自定义环境变量
vue CLI:process.env.VUE_APP_BASE_URL

# vue 语法
createApp():创建一个Vue应用实例，返回一个应用实例对象 应用级
app.mount():将应用实例挂载到DOM元素上，返回组件实例对象 组件级

## template语法
一种基于 HTML 的模板语法，使我们能够**声明式**地将其**组件实例的数据绑定到呈现的 DOM 上**
1. 文本插值 {{}}插值语法 模版语法
2. 指令:扩展HTML tag的属性 支持js表达式
v-if  v-for
v-model:双向数据绑定
v-on:事件监听
v-html:插入html
v-bind:动态绑定html属性或者组件props <div v-bind:id="dynamicId"></div> -->简写为 <div :id="dynamicId"></div> -->同名简写为<div :id></div>

v-loading
v-slot

指令的参数通过:来指定，例如v-bind:src="imageSrc" 
<a v-bind:[attributeName]="url"> ... </a>动态参数绑定 attributeName会被作为一个变量解析，它的值会作为最终的参数传递给指令。例如，如果 attributeName 的值为 "href"，则等同于 v-bind:href。

指令的修饰符通过.来指定，例如v-on:click.stop
<a v-on:click.stop="doThis"> ... </a>修饰符可以串联使用，例如v-on:click.stop.prevent
<a v-on:click.stop.prevent="doThis"> ... </a>

![alt text](指令语法.png)

## 响应式基础
依赖追踪的响应式系统

// 伪代码，不是真正的实现
const myRef = {
  _value: 0,
  get value() {
    track()
    return this._value
  },
  set value(newValue) {
    this._value = newValue
    trigger()
  }
}

ref():创建一个响应式引用，返回一个包含value属性的对象, 是一个wrapper,它包装了一个值，并提供了一个访问该值的响应式接口。
	在标准的 JavaScript 中，检测普通变量的访问或修改是行不通的。然而，我们可以通过 getter 和 setter 方法来拦截对象属性的 get 和 set 操作。Vue 的响应式系统正是利用了这种拦截机制，通过使用 Object.defineProperty() 方法来定义 getter 和 setter，从而实现对数据的响应式处理。
	是一个wrapper，底层实际是个globalthis.Ref对象

script setup:
	在 setup() 函数中手动暴露大量的状态和方法非常繁琐 
	幸运的是，我们可以通过使用单文件组件 (SFC) 来避免这种情况。我们可以使用 script setup 来大幅度地简化代码
	script setup 是 Vue 3.2 中引入的一个新特性，它允许我们在单文件组件中编写更简洁的代码，并自动将组件的状态和方法暴露给模板使用。顶层的导入、变量、函数和常量都会自动暴露给模板使用，你可以理解为模板是在同一作用域内声明的一个 JavaScript 函数——它自然可以访问与它一起声明的所有内容。


reactive():创建一个响应式对象，返回一个响应式代理对象proxy, 直接将一个对象转换为响应式代理，而无需显式地创建一个 ref 对象。
		仅支持对象类型，不能用于原始类型，例如字符串、数字、布尔值等。
		对解构操作不友好，解构后的对象将失去响应性。

nextTick():在下一个 DOM 更新周期之后执行延迟回调。在更改数据之后立即使用它，然后等待 DOM 更新。它通常用于在数据更改后立即访问更新后的 DOM。

## 计算属性
使用计算属性来描述依赖响应式状态的复杂逻辑
computed():期望接收一个getter函数，创建一个计算属性，返回一个计算属性ref对象，计算属性会根据其依赖的响应式状态自动更新
响应式依赖：计算属性会根据其依赖的响应式状态自动更新，当依赖的状态发生变化时，计算属性会重新计算并更新其值。

## 事件处理
v-on:click="handler" 简写为@click="handler"
1. 内联事件处理器,直接在模板中编写事件处理函数，简单场景
2. 方法事件处理器,定义一个函数，并在模板中引用该函数，复杂场景
3. 事件修饰符,例如.stop、.prevent、.capture、.self、.once、.passive等，用于处理事件冒泡、默认行为、事件捕获、事件自身、事件只触发一次、事件被调用后立即执行等场景
4. 按键修饰符,例如.enter、.tab、.delete (捕获“删除”和“退格”键)、.esc、.space、.up、.down、.left、.right等，用于处理键盘事件
5. 系统修饰键,例如.ctrl、.alt、.shift、.meta等，用于处理组合键事件
6. 鼠标修饰符,例如.left、.right、.middle等，用于处理鼠标事件

## 表单输入绑定
v-model:双向数据绑定，用于在表单输入元素上创建双向数据绑定，将表单输入元素的值与组件的数据属性进行绑定，当表单输入元素的值发生变化时，组件的数据属性也会相应地更新，反之亦然。
v-model.lazy:在输入框失去焦点时才更新数据，而不是在每次输入时都更新数据。
v-model.number:将输入的值转换为数字类型。
v-model.trim:去除输入值的前后空格。

表单元素包括form input textarea select label output等

'''
<script setup>
import { ref } from 'vue'

const messageRef = ref('测试')
</script>

<template>
  <p>Message is: {{ messageRef }}</p>
	<input v-model="messageRef" placeholder="edit me" />
</template>
'''

## 模板引用
模板引用区别于响应式引用，模板引用是直接访问DOM元素或组件实例的引用，可以在模板中使用ref属性来标识一个DOM元素或组件实例，然后在JavaScript代码中使用this.$refs来访问该引用。
vue抽象了大部分对DOM的操作,但有时我们需要直接访问DOM元素，可以使用模板引用来获取DOM元素, 
ref attribute是一个HTML tag的特殊属性,可以用来标识一个tag,类似于id,但ref是vue特有的，只能在vue组件中使用

组合式API中，使用useTemplateRef()来获取模板引用
选项式API中，使用this.$refs来获取模板引用

也可以获得一个组件的ref,如下所示:

'''
<script setup>
import { useTemplateRef, onMounted } from 'vue'
import Child from './Child.vue'

const childRef = useTemplateRef('child')

onMounted(() => {
  // childRef.value 将持有 <Child /> 的实例
})
</script>

<template>
  <Child ref="child" />
</template>
'''

## 深入组件
1. 组件是可复用的 Vue 实例，且带有一个名字,对HTML tag的扩展
2. props:组件的属性，用于接收父组件传递的数据，props是单向数据流，即父组件的数据流向子组件，子组件不能修改父组件的数据,是一种特殊的atttribute,对HTML tag属性的扩展
3. 透传attribute指的是传递给一个组件，却没有被该组件声明为 props 或 emits 的 attribute 或者 v-on 事件监听器。最常见的例子就是 class、style 和 id。

'''
BlogPost.vue
<script>
export default {
  props: ['PropName']
}
</script>

<template>
  <h4>{{ PropName }}</h4>
</template>

父组件
<BlogPost PropName="My blog post" class="blog-post" /> //自定义的attribute
<BlogPost
  v-for="post in posts"
  :key="post.id"
  :PropName="post.title"
 />
'''

4. 事件:子组件可以通过 $emit 方法来触发事件，父组件可以通过 v-on 或 @ 来监听子组件的事件。
5. 插槽:插槽是 Vue 组件中用于分发内容的机制，允许我们在组件中插入自定义的内容。插槽可以通过 v-slot 指令来定义，也可以通过 <slot> 标签来定义。
6. vue组件名推荐使用CamelCase以区别于HTML原生tag，如BlogPost，而不是blog-post
7. prop名字在js上使用camelCase，如propName，为了和HTML原生attribute对齐(不区分大小写)，vue内部会自动转为kebab-case，如prop-name,在模板中使用时，需要使用kebab-case，如prop-name
8. Vue 中的 prop 名称转换是一个自动过程，遵循以下规则：

	- 在组件定义中使用驼峰命名法（camelCase）
	- 在 HTML 模板中使用短横线命名法（kebab-case）
	- Vue 会自动处理这两种命名法之间的转换

9. props需要逐级传递，链路很长时，可能需要传递很多props，可以使用provide/inject来简化
10. 透传attribute
11. 插槽slot，前面的都是传递javascript类型，slot可以接受模板内容，可以理解为传递HTML类型，即子组件渲染外层的HTMLtag，里面的内容由父组件提供，并渲染在slot位置

v-bind:绑定属性
v-model:是v-bind:value和v-on:xx的语法糖，用于在表单输入元素上创建双向数据绑定，将表单输入元素的值与组件的数据属性进行绑定，当表单输入元素的值发生变化时，组件的数据属性也会相应地更新，反之亦然。

问题:
${id}
@click="doThis" 
$emit

user?.id 可选链操作符，用于访问嵌套对象的属性，如果对象为null或undefined，则返回undefined，而不是抛出错误。
?:空值合并操作符，用于为变量提供一个默认值，如果变量为null或undefined，则返回默认值，而不是undefined。

defineProps()和defineEmits()是Vue 3.2引入的Composition API，用于在setup函数中定义组件的props和emits。

this

cur = getCurrentInstance()是Vue 3.0引入的一个全局API，用于在setup函数中获取当前正在执行当前代码的那个组件实例。
cur.parent是获取当前组件实例的父组件实例，cur.proxy是获取当前组件实例的代理对象，cur.root是获取当前组件实例的根组件实例。
ref() toRefs() 

Vue 3 中，可以通过 app.config.globalProperties 来注册全局属性，这些属性可以在所有组件中通过组件实例的代理对象访问

createAPP()是Vue 3.0引入的一个全局API，用于创建Vue应用实例。它接受一个选项对象作为参数，并返回一个应用实例。应用实例提供了一些方法，例如mount、unmount、provide、inject等，用于管理应用的生命周期和状态。

app.config.globalProperties.useDict = useDict可以挂载全局属性或者函数，可在组件内通过proxy.useDict访问

emit:用于触发自定义事件(就是个字符串)，可以传递参数给事件监听器。

### 插槽
在某些场景中，我们可能想要为子组件传递一些模板片段，让子组件在它们的组件中渲染这些片段。这就是插槽（slot）的用途。

插槽是 Vue 组件中用于分发内容的机制，允许我们在组件中插入自定义的内容。

在子组件的template片段中，通过<slot>标签来定义插槽，插槽可以包含默认内容。
<slot name="header">默认内容</slot>

在父组件中使用子组件时可以通过 v-slot 指令来指定哪个slot, 旧版本用slot-scope。

插槽分为默认插槽和具名插槽。默认插槽名为default，只有一个，而具名插槽可以有多个，每个具名插槽都有一个名字。

v-slot:插槽名，也可以简写为 #插槽名，插槽名可以省略，默认为default
v-slot:[dynamicSlotName] #[dynamicSlotName]，动态插槽名，可以在v-slot指令中动态指定插槽名

父组件通过插槽内容来填充插槽，插槽内容可以是**任何合法的模板内容**，包括HTML标签、文本、指令甚至vue组件等。插槽内容是在父组件定义的，可以访问父组件作用域，无法访问子组件作用域

slot 元素是一个插槽出口 (slot outlet)，标示了父元素提供的插槽内容 (slot content) 将在哪里被渲染。

还可以使用条件插槽 v-if="$slots.header"

**作用域插槽**，子组件可以通过 slot element tag的属性来向插槽内容传递数据，父组件可以通过 v-slot 指令来接收这些数据。
可以像对组件传递 props 那样，向一个插槽的出口上传递 attributes
<slot :text="greetingMessage" :count="1"></slot>

内部实现原理:
MyComponent({
  // 类比默认插槽，将其想成一个函数
  default: (slotProps) => {
    return `${slotProps.text} ${slotProps.count}`
  }
})

function MyComponent(slots) {
  const greetingMessage = 'hello'
  return `<div>${
    // 在插槽函数调用时传入 props
    slots.default({ text: greetingMessage, count: 1 })
  }</div>`
}

"'
BaseLayout.vue
<template>
  <div class="container">
    <header>
      <slot name="header"></slot>
    </header>
    <main>
      <slot></slot>
    </main>
    <footer>
      <slot name="footer"></slot>
    </footer>
  </div>
</template>

<style>
  footer {
    border-top: 1px solid #ccc;
    color: #666;
    font-size: 0.8em;
  }
</style>


App.vue
<script>
import BaseLayout from './BaseLayout.vue'
  
export default {
  components: {
    BaseLayout
  }
}
</script>

<template>
  <BaseLayout>
    <template v-slot:header>
      <h1>Here might be a page title</h1>
    </template>

    <template v-slot:default>
      <p>A paragraph for the main content.</p>
      <p>And another one.</p>
    </template>

    <template #footer>
      <p>Here's some contact info</p>
    </template>
  </BaseLayout>
</template>

'"

**组件实例的属性**:
$data:组件实例的响应式数据对象,data()函数返回的对象,组件内部的状态，作用域限于组件内
$props:组件实例的props对象，对HTML tag attribute的扩展，可以静态(id="123")或动态(:id="123")绑定,用于父组件向子组件传递数据
$el:应用实例挂载的DOM元素根节点,3.1+废除了(支持fragment，多个根节点)
$options:组件实例的选项对象
$parent:组件实例的父组件实例
$root:组件实例的根组件实例
$refs:组件实例的模板引用对象(应该是所有模板引用的集合)
$slots:组件实例的插槽对象
$attrs:组件实例的attribute对象
$emit:组件实例的自定义事件触发器，向父组件发送事件
$watch:组件实例的响应式数据监听器
$nextTick:组件实例的DOM更新队列

vue父子组件间的数据传递和通信，下面是一个详细的总结，包括数据传递和通信方式：
 1. **父组件向子组件传递数据（Props Down）**
    - 父组件通过`props`向子组件传递数据。
    - 子组件中通过`props`选项声明接收的数据。
 2. **子组件向父组件发送消息（Events Up）**
    - 子组件通过`$emit`触发事件，父组件通过`v-on`（或`@`）监听事件。
 3. **父组件访问子组件（Ref）**
    - 父组件可以通过`ref`属性获取子组件的引用，然后直接访问子组件的属性和方法（但不推荐直接修改子组件的数据，应通过props和事件进行通信）。
 4. **子组件访问父组件**
    - 子组件可以通过`$parent`访问父组件实例，但同样不推荐，因为这样会破坏组件的封装性。
 5. **跨层级组件通信（Provide/Inject）**
    - 祖先组件通过`provide`提供数据，后代组件通过`inject`注入数据。但同样需要注意，这也会使组件的复用性降低。
 6. **状态管理（Vuex/Pinia）**
    - 对于复杂的应用，推荐使用状态管理库（如Vuex或Pinia）来管理共享状态。

## 内置指令
v-text:用于设置元素的文本内容，可以用来代替元素的textContent属性。等价于 {{ }} 插值语法。
v-html:用于设置元素的HTML内容，可以用来代替元素的innerHTML属性。

v-show:通过设置内联样式的display属性来工作
v-if:用于条件渲染，根据表达式的值来决定是否渲染元素。
v-else-if:用于条件渲染，与v-if一起使用，表示当v-if的条件不成立时，继续判断v-else-if的条件。

v-for:用于循环渲染元素，可以用来遍历数组、对象或数字。

v-on:给元素绑定事件监听器，可以简写为@,当用于普通元素，只监听原生 DOM 事件。当用于自定义元素组件，则监听子组件触发的自定义事件。修饰符：.stop、.prevent、.capture、.self、.once、.passive .left .right .middle 

v-bind:用于绑定一个或多个属性或一个组件prop到表达式，可以简写为:，当用于普通元素，可以绑定任何属性，当用于自定义元素组件，则绑定组件prop。修饰符：.prop、.camel、.sync
-	当用于组件 props 绑定时，所绑定的 props 必须在子组件中已被正确声明。
-	当不带参数使用时，可以用于绑定一个包含了多个 attribute 名称-绑定值对的对象

v-model:用于在表单输入元素或组件上创建双向数据绑定，可以简写为v-model，修饰符：.lazy、.number、.trim

v-slot:用于声明具名插槽或是期望接收 props 的作用域插槽，可以简写为#，用于在组件上声明插槽，也可以用于在组件上声明作用域插槽。在 template 上使用

v-pre:跳过该元素及其子元素的编译过程，用于提高性能。
v-once:只渲染元素和组件一次，即使随后的重新渲染发生，该元素或组件及其所有的子节点仍按原样渲染，不会进行更新。
v-memo:用于缓存一个模板的渲染结果，只有当依赖项发生变化时才会重新渲染，用于提高性能。
v-cloak:在编译结束后，该指令会被移除，常用于解决在页面加载时出现闪烁的问题。


## 内置组件
<component>:用于动态地渲染组件，可以用来根据条件渲染不同的组件。
<transition>:用于在元素或组件的插入、更新或移除时应用过渡效果。
<transition-group>:用于在元素或组件的插入、更新或移除时应用过渡效果，适用于多个元素或组件。
<keep-alive>:用于缓存组件实例，避免在切换时重新渲染组件。
<teleport>:用于将组件渲染到指定的DOM节点中，常用于模态框、通知等需要脱离当前组件上下文的场景。

## 三方库
vue库:
axios:http请求库 url是啥含义
vue-router:路由库
vuex:状态管理库
pinia:状态管理库 比vuex轻量易用
	1. 实例化 app = createApp(App); pinia = createPinia(); app.use(pinia);
	2. 创建/使用仓库store,其中保存了状态和函数 useCounterStore = defineStore('counter'); counterStore = useCounterStore();
vue-cli:脚手架工具
vue-devtools:浏览器插件，用于调试Vue应用
vue-loader:webpack插件，用于加载.vue文件
vue-test-utils:用于测试Vue组件的库
vue-apollo:用于与Apollo GraphQL API进行交互的库
vue-i18n:用于实现国际化功能的库
js-cookie:用于操作浏览器cookie的库