# Vue 指令
+ v-bind 属性绑定
    - 主要用于绑定DOM元素的属性，将变量通过bind绑定到DOM元素上。
    - 单向绑定，不能实现双向绑定。
    - 可以将 `v-bind` 缩写为 : 。
+ v-text 文本绑定
    - 主要用于绑定变量到DOM元素内部，将变量作为字符串传入进去。
    - 同样的，v-text 也不能用于双向绑定，且会覆盖DOM元素原先的children。
    - 没有缩写。
+ v-html  主要用于 html 绑定
    - 主要用于绑定变量到DOM元素内部，与 `v-text` 不同的格式，`v-html` 可以将字符串中的html标签解析出来。
    - 同样的，`v-html` 也不能用于双向绑定，且会覆盖DOM元素原先的children。
    - 没有缩写。
+ {{ }} 主要用于属性计算或者属性判断
    - 双括号主要用于将变量绑定到DOM元素内部，与`v-text`的功能相当。
    - 与 `v-text` 不同的是，双大括号可用于DOM元素内部的字符串拼接，不会覆盖DOM元素原先的children。
    - 缺点是 如果网速过慢导致 js加载延迟，则会在页面上显示出`{{msg}}`，等待js加载完成并执行之后，才会显示出真正的变量值。
    - 这种缺点可以通过给DOM元素添加 `v-clock` 来解决，`v-clock` 会在变量解析为变量值的时候在DOM元素上被清除，所以可以定义css `[v-clock]{display:none}`，在js为解析前，让包含{{}}的元素默认隐藏，等解析完成之后再显示出来。
    - 双大括号中可以写 变量、算数表达式、三目运算符、链式调用 等，其他js表达式则不能生效。

+ v-model 双向数据绑定
    - vue 双向绑定，根据 Object.defineProperty 的setter ，getter 来监听数据的改变。
    - v-model 是Vue中惟一的双向数据绑定指令，常用于`input`、`select`、`textarea` 等可以输入操作的控件中。当你输入的时候修改Vue中的变量。
    - v-model 没有缩写。

+ 类名绑定 v-bind:class
    - 不存在 v-class。
    - 一种是 数组形式 eg: `v-bind:class = "[class1,class2?,"class3"]"`。 此时 class1 为变量 ，class3 为常量。
    - 一种是 对象形式 eg：`v-bind:class = "{class1:true,class2:true?true:false,class3}"`。 class1 ，class2，class3 都是常量。

+ 样式绑定 v-bind:style
    - 不存在 v-style。
    - 对象 ，eg:  `v-bind:style = "{width:'20px',textAlign:'center'}"`,  如果 样式的键 中有 - ，则需要将其转换为小驼峰命名法，首字母为小写，之后每个单词的首字母为大写。
    - 数组， eg: `v-bind:style = "[style1,style2]"`。
    - 自动绑定前缀， eg: `v-bind:style = "[]"`

+ v-once 结合 {{}}使用
    - 非双向绑定。
    - 只执行一次插值，之后不再依赖变量的改变而改变。

+ v-on 事件绑定
    - 可以简写为 @。
    - eg ： `<button @click = "click">按钮<button/>`。

+ 变量修饰符 结合`v-model`
    - `.nember` 可以将输入的值转化为数字。 eg:`v-model.number`
    - `.lazy`  可以将input等输入元素的变量同步时机从 `oninput` 改为 `onchange`。当具体值改变的时候才触发。
    - `.trim` 可以去除掉输入值的前后端的空格。

+ 事件修饰符  eg： `@click.stop  ` 可以链式调用，但是对顺序有要求，顺序不同，产生的效果也不同
    - `stop` 阻止冒泡 
    -  `prevent` 阻止默认事件
    - `aptuare` 在捕获阶段执行 
    - `once` 只执行一次
    - `self` 当 `e.target` 为元素自身的时候调用。
    - `native` 在根元素上监听事件。

+ 按键修饰符
    - `keyup.alt.67` 即按着`alt`键，按下`67`键。

+ 系统修饰符
    - `@click.ctrl` 按着`ctrl` 点击鼠标。

+ v-if v-else v-else-if 条件判定
    - `v-else` `v-else-if` 必须跟在`v-if` 后边。 
    - 判断满足条件之后才渲染。

+ v-for 循环
    - `v-for` 循环数组。 与 `v-if` 一起使用 存在冲突，`v-for` 的优先级大于 `v-if`。如果需要使用if，则最好用`computed` 计算属性将迭代数组根据`v-if`条件过滤。
    - 由于 Vue 的组件复用机制，请视情况选择添加 key属性， `v-bind:key`.

+ v-show 显示
    - `v-show` 通过修改 组件的 `display` ， 在 `block` 与 `none` 中转换。 

# Vue 自定义指令

+ 通过 `Vue.directive(name,options)`.
    - `name` 定义的指令。
    - `option` 的组成。
        - 状态，值是一个回调函数，，在函数中去执行相应的操作。
        - 可根据不同的状态去定义不同的回调函数来调用，执行不同的操作。

+ 钩子函数
    - `bind`,第一次绑定到元素上的时候调用，只调用一次。多用于初始化的时候。
    - `inserted` 即在组件插入到父元素之后，触发这个函数。
    - `update` 当被绑定模板更新时调用。
    - `componentUpdated` 被绑定元素所在模板完成一次更新周期时调用。
    - `unbind` 只调用一次， 指令与元素解绑时调用。

+ 钩子函数参数
    - `el` 指令绑定的元素，可用于直接操作DOM。
    - `binding` 一个对象，包含以下几点
        - `name` 指令名，不包含`v-`
    - `vnode` 编译生成的虚拟节点。
    - `oldVnode` 上一个虚拟节点，仅在 `update`,`componentUpdated` 中使用。
# Vue 属性

+ `computed 计算属性`
    - 一般情况下是为了简写插值表达式，将html中的插值表达式中的js表达式转移到 computed中。
    - 一般定的规则是用于 变量的`getter`方法。即在变量取值的时候执行计算属性定义的响应函数。
    - `computed` 依赖缓存，当变量依赖于其他变量时，如果其他变量都没变，则计算属性也不会改变，当其依赖变量改变时，该计算属性也会做出相应的计算并改变，否则就基于他的依赖缓存取值。
    - `computed`属性定义的函数一般指定的是属性的`gutter`，如果需要也可以定义属性的`setter`，可以在属性赋值的时候，做一些其他的事情。`getter`函数也要单独作为`get`方法定义在属性上，`setter`函数作为 `set`方法定义在属性上。
 
+ `methods 方法`
    - `html`中的插值也可以通过直接调用 methods中的方法来获取值。
    - `methods` 与 `computed` 的区别在于，`computed`只有在当依赖变量改变时才会重新求值。而`methods`会在每次重新加载时都活重新执行。
    - 总的来说。`computed` 比 `methods`的性能好一点，但如果你不希望使用缓存的时候，`methods`将会是你最好的选择。

+ `watch 监听属性`
    - 用于对 计算属性的补充，即当属性改变时，如果发生比较多的关联操作时，就会用到`watch`属性,比如 当属性改变时涉及`ajax`操作等。
    - watch 属性有两个值，分别是oldval 和val ，以此来做响应的操作。
    - 不要滥用，`computed` 和`methods` 基本满足日常需要。

+ `data 组件的值。`
    - 当组件为单一组件时，可以将data直接设置为 对象。
    - 当组件可以复用的时候，data必须作为一个返回一个对象的函数来使用。否则会导致所有引用该组件的地方的状态同时被改变。
    - 正常情况下，使用函数返回对象的方法替代直接定义对象。

# Vue 组件 component

+   `全局定义组件`
    - 使用 `Vue.Component(name,options)` 来定义组件。`name` 为 组件的名称.
    -  `options` 的构成 
        - `template` html模板。
        - `props` 传递进来的属性数组。
        - `data` 一个返回对象的函数，作为组件本身的状态，必须是一个函数。
        - `methods` 组件中的方法，和 Vue 中相似。
        - `watch` 属性监听，和 Vue 类似。
        - `computed` 计算属性，和 Vue中的computed类似。
+ `局部组件`
    - 局部组件，即在当前实例中可用的组件，不使用`Vue.component` 创建, 使用 对象字面量形式创建。
    - eg：`var newcomponent = {template:'<p>z这里是局部组件</p>}`。构成和全局组件的构成相似。

+ `props 验证规则`
    - eg： `props:{propname1:{type:String,required:true,default:'sdd'},propname2:String}`

+ `自定义事件` - 组件的prop 是通过 父组件传入进去的，如果在子组件中，需要修改传入的变量，并把变量传递回父组件，那么就需要自定义事件。
    -  说白了，自定义事件就是要通过触发自定义事件，进而触发父组件中定义的修改父组件状态的方法，从而达到子组件修改父组件的功能实现。
    - eg： 子组件 定义属性 `v-on:hahaha = parentEvent`, 在子组件的html元素上定义`v-on:click = checkthis`, 在`checkthis`中 执行`$emit('hahaha')`,这样就可以执行父组件中定义的`parentEvent`方法。
