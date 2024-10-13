# 1.模板语法

## 1.1声明式渲染

声明式是指可以像“声明变量”那样表示⻚面结构和绑定⻚面中的数据。Vue.js 基于标准 HTML拓展了一套模板语法，因此可以声明式地描述最终输出的 HTMl和JavaScript状态之间的关系。

```vue
<template>
    <div>
        {{ message }}
    </div>
</template>
<script setup>
import {ref} from 'vue'
const message = ref('hello world')
</script>
```

`上述代码声明了一个<div>元素，并用双花括号 {{ }} 包裹数据 message，表示元素内容。在默认情况下，"{{message}}"只是普通文本，如果要将其变成真实数据，则需要使用Vue.js3提供的createApp()方法创建一个Vue.js实例，并挂载在应用的根元素上。`

```js
import { createApp } from 'vue'

import App from './App.vue'

createApp(App).mount('#app')
```

在App.vue中引入这个组件

```vue
<template>
  <div>
    <Monkey7/>
  </div>
</template>

<script setup lang="ts">
import example1 from './components/example1.vue';
</script>
<style scoped>
</style>
```

![avatar](https://s2.loli.net/2024/10/10/GBmjHyiDWrA1546.png)

## 1.2组件系统

组件化是Vue.js的另一个核心。组件可以将庞大的项目工程拆分为独立的模块，从而降低代码的耦合性。一些公共的UI或逻辑也可以拆分为公共组件在多处复用。虽然组件之间默认互相隔离但是可以在组件之间共享数据。在不同类型的项目中，组件是以不同的形式存在的。Vue.js的两种集成方式如下：

普通项目集成：在HTML中直接引入Vue.js文件；

工程化项目集成：通过npm命令安装 Vue.js模块。

组件的代码结构从整体上来看可以分为 3个区域。

```
<template></template>：模板区域，基于HTML，声明式地绑定数据，表示⻚面结构；

<script></script>：脚本区域，提供主要的数据和方法等；

<style></style>：样式区域，用来修饰模板的样式
```

# 2.Vue.js的基础概念

## 2.1插值语法

插值语法用于在模板中将Vue的响应式数据绑定到 DOM中，最常⻅的方式是使用双花括号{{}}，它可以将组件的状态动态插入到HTML中。

```vue
<template>
    <div>
        <h2>{{userName}}</h2>
    </div>
</template>

<script setup lang="ts">
import {ref} from 'vue'
const userName = ref<string>('张三')
</script>
```

![e460332df1116367d32fb4e41e5c5619](https://s2.loli.net/2024/10/10/cU5YJ1OfBZDqRjp.png)

可在插值表达式中进行计算，和字符串连接

![4d2fc6745cd1f4fbf7b5087421906131](https://s2.loli.net/2024/10/10/fFQ5C3HEUZI7oew.png)

## 2.2属性绑定

在Vue3中，v-bind可以直接绑定一个变量到HTML元素的属性上。例如，我们可以动态绑定一个布尔值来控制按钮是否禁用，可用语法糖：来表示。

### 如图展示式绑定一个对象。

![c8ddd12f74725f15386b6149000771d5](https://s2.loli.net/2024/10/10/8VNHFJikIAwx1CT.png)

### 类绑定

![e3b14db7a7f0f7a888ea780221ddbb86](https://s2.loli.net/2024/10/10/bTvdVUB3HJ2Pc7a.png)

切换后

![59508d50649b99f3b1c2fa4dd98cb7db](https://s2.loli.net/2024/10/10/iuUwZeWGb45LX3A.png)

### style绑定

![304ab1d14d133330bb0fa86f4ecacec8](https://s2.loli.net/2024/10/10/OWLxGc3t1HIJPbU.png)

切换后

![bd423f5393eb04517fc1084ddb70fea9](https://s2.loli.net/2024/10/10/U6iAryx7HFhkQ3f.png)

### 动态绑定自定义的属性





# 3.状态和方法



## 3.1状态

`在Vue3中，状态可以通过ref或reactive进行定义，这两者都可以使数据具有响应式的能力。当状态数据发生改变时，Vue会自动重新渲染视图。ref：适用于基本数据类型（如number、string、boolean）以及简单对象。ref包装了一个值，并通过.value来访问或修改这个值。reactive：适用于复杂对象（如数组、对象）。reactive将整个对象转换为响应式的，当对象的任一属性发生改变时，Vue会自动追踪这些变化。`

### 用ref定义简单状态

![049adccd1402e2e8435c3f7b46bf2b5f](https://s2.loli.net/2024/10/10/5xM4bKmZticlAde.png)

count是一个ref，它包裹了一个数字类型的状态。初始值为 0，类型为number；通过count.value++修改状态，Vue会自动更新视图

### 使用reactive定义复杂状态

![bde6f391afd0e5124fd09feb7b4dd4fc](https://s2.loli.net/2024/10/10/FgIjYUJ6CcT1xRv.png)

user是一个响应式对象，使用reactive定义并指定了类型{ name: string; age: number }；当修改user.age时，Vue会追踪变化并自动更新相关视图

## 3.2方法

`在Vue3的<script setup>中，方法通常是以函数的形式定义，可以直接修改组件的状态或执行其他操作。结合TypeScript，可以为方法指定参数和返回值的类型，确保代码的安全性和可读性`

###  定义无参数方法

![image.png](https://s2.loli.net/2024/10/10/WD1wGnZAr8bsoEh.png)

### 定义带参数的方法

![image.png](https://s2.loli.net/2024/10/10/apljIw6gALkPYnc.png)

### 状态与方法的结合使用

![image.png](https://s2.loli.net/2024/10/10/zDrKhxGWailXVe3.png)

`user是一个响应式对象，包含name和age属性；changeName方法接受一个newName参数来动态修改用户名；resetUser方法重置用户信息，将用户数据恢复到初始状态。`

# 4.条件渲染与列表渲染

## 4.1条件渲染

`在Vue中，使用v-if、v-else-if、v-else指令来实现条件渲染。v-if：仅当条件为true时渲染元素。v-else-if：为多个条件分支提供支持。v-else：当所有v-if和v-else-if条件为false时，渲染v-else。`

`使用isVisible状态来控制文本的显示与隐藏；当点击按钮时，调用toggleVisibility方法，切换isVisible的值，并且根据其值显示不同的文本`

![image.png](https://s2.loli.net/2024/10/10/p6SOrVZ9I2X8Yjk.png)

使用v-if、v-else-if和v-else结合，展示不同年龄段的提示；通过按钮点击增加userAge的值，并动态更新显示的内容。

![image.png](https://s2.loli.net/2024/10/10/NGZQkIsCTDdwl1E.png)
## 4.2列表渲染

列表渲染用于根据数组或对象的数据，动态渲染一组元素。Vue通过v-for指令来实现列表渲染。用于遍历数组、对象或指定的次数，生成对应的元素

![image.png](https://s2.loli.net/2024/10/10/bZD4jSOqfyJUNwv.png)

使用v-for遍历items数组，并为每个项目生成一个li标签；:key是唯一标识符，用于优化Vue的虚拟DOM渲染。





当我们渲染一个对象数组时，可以通过v-for遍历每个对象，并使用模板语法展示对象的属性。

![image.png](https://s2.loli.net/2024/10/10/bZD4jSOqfyJUNwv.png)
## 4.3条件渲染与列表渲染结合

在实际项目中，条件渲染和列表渲染经常结合使用。可以根据某些条件决定是否渲染整个列表，或者在列表中根据不同条件渲染不同的内容。

![image.png](https://s2.loli.net/2024/10/10/UFpv91RjINMKYCd.png)
使用v-if和v-else根据用户的年龄渲染不同的文本（成人或未成年）；列表项中的每个用户根据其年龄不同展示不同的内容。

# 5.计算属性与监听器

## 5.1计算属性

`在Vue3中，通过computed函数来定义计算属性。在<script setup>中，计算属性和状态可以直接在同一作用域中定义，并且使用 TypeScript可以为计算属性的返回值定义类型`

例子:

![image.png](https://s2.loli.net/2024/10/10/XZ4JO7qPI5oTMhS.png)

price和discount是两个响应式状态；计算属性discountedPrice根据price和discount计算折后价格，当price或discount变化时，discountedPrice自动更新；

在TypeScript中，可以为计算属性的返回值显式声明类型，以确保代码的类型安全。

```vue
const yearlySalary = computed<number>(()=>{return monthlySalary.value*12})
```

## 5.2监听器

监听器用于监听响应式数据的变化，并在变化时执行特定的副作用函数。它通常用于处理需要响应数据变化的复杂逻辑，特别是副作用（例如，发送 API 请求、日志记录、处理深层次对象等）。

监听器不会自动缓存，因此每次数据变化时都会触发。

简单监听：监听单个状态的变化。

深度监听：监听对象或数组中的嵌套属性的变化。

在Vue3中，使用watch函数来监听响应式状态或计算属性的变化，并执行相关逻辑

### 监听单个状态

![image.png](https://s2.loli.net/2024/10/10/Udq5oSwIDnB7NZl.png)

searchQuery是输入框绑定的响应式状态；监听器watch监听searchQuery的变化，并输出新旧值的变化记录

### 监听多个状态

![image.png](https://s2.loli.net/2024/10/10/72nx4vYb6KEekoG.png)
通过watch([firstName, lastName])监听firstName和lastName的变化，并打印全名变化。当需要监听对象或数组中的嵌套属性时，必须使用深度监听。通过在watch的第三个参数中设置deep: true来启用深度监听

![image.png](https://s2.loli.net/2024/10/10/2pdDTQXsv89efOq.png)

```
监听器默认情况下是在被监听的数据发生变化时才会触发。如果希望监听器在绑定时立即执行，可以通过immediate: true选项
```

# 6.事件处理

事件处理指的是在Vue模板中监听DOM事件，并在事件触发时调用对应的方法。常⻅的事件有click、input、submit等。

使用v-on绑定事件，通常简写为@。

事件处理器通常是组件中的方法或匿名函数。

在Vue中，最常⻅的事件是click事件。可以通过v-on:click或其缩写@click来监听按钮或其他元素的点击事件

### 6.1@click用于监听按钮的点击事件

```
<button @click="handleClick">点击获取鼠标坐标</button>
```

在事件处理器中，可以访问原生的事件对象（如MouseEvent、KeyboardEvent等）。通过将事件对象作为参数传递给处理器，能够获取到更多关于事件的详细信息

### 6.2事件修饰符

Vue提供了一些常用的事件修饰符，可以简化事件处理的逻辑，例如阻止默认行为或事件冒泡。.prevent用于阻止元素的默认行为，等同于调用event.preventDefault()

@submit.prevent阻止了表单的默认提交行为（⻚面刷新）

@click.stop阻止了按钮点击事件向外层div冒泡

Vue提供了按键修饰符，可以方便地处理键盘事件。例如，捕获回⻋键、Esc键等特殊键的输入。.enter监听Enter键的按下，适用于输入表单或其他键盘交互

# 7.表单的双向绑定

在Vue3中，表单双向绑定通过v-model指令实现，它允许将表单元素（如输入框、复选框、下拉菜单等）的值与Vue组件中的数据进行同步。通过v-model，可以实现数据在模板和组件状态之间的双向绑定，这使得数据的变化能够立即反映在 UI 上，反之亦然

### 7.1单个绑定

例子:

![image.png](https://s2.loli.net/2024/10/10/HmpR9EJWlTDwN5Z.png)

v-model不仅可以应用于文本输入框，还可以应用于复选框、单选框、选择框等多种表单控件。 

### 7.2多个复选框绑定

![image.png](https://s2.loli.net/2024/10/10/ipM4R9AoLVWH37K.png)

### 7.3修饰符

Vue3中的v-model提供了许多修饰符，用于更细粒度地控制双向绑定的行为。常⻅的修饰符有.lazy、.number和.trim。默认情况下，v-model会在input事件中同步数据，但

使用.lazy修饰符可以延迟到change事件时才同步数据。

使用.number修饰符，确保用户输入的内容会自动转换为数字类型并同步到age状态中

.trim修饰符可以用于自动删除用户输入中的首尾空格。



### 7.4多v-model绑定语法

除了在原生HTML表单元素上使用v-model，我们还可以在自定义组件中使用v-model。自定义组件中的v-model会默认绑定到modelValue属性，并通过update:modelValue事件来更新数据

多model绑定需要

```
v-model：你要绑定的值    在父组件中
```

基本用法：v-model提供了双向绑定功能，可以在表单元素（如文本框、复选框、单选按钮、下拉菜单）中实现数据同步。修饰符：可以使用.lazy、.number和.trim修饰符来控制双向绑定的行为，如延迟同步、自动类型转换、删除空格等。多个复选框：通过将多个复选框绑定到数组，管理多个选项的选择。自定义组件中的v-model：可以在自定义组件中使用v-model，并通过modelValue和update:modelValue事件来实现双向绑定。多绑定：Vue3支持为同一组件中的多个值使用v-model，通过不同的v-model语法实现对多个值的双向绑定。通过对v-model的掌握，我们能够轻松实现表单的双向数据绑定，并通过修饰符、自定义组件的使用，进一步增强表单数据管理的灵活性

# 8.DOM操作

Vue3中的DOM操作通常依赖Vue的模板语法和响应式数据绑定来自动更新 DOM。但在某些特殊情况下，我们可能需要手动操作 DOM 元素，比如需要访问或直接操作底层的 HTML元素属性时，Vue提供了相应的工具（如ref和生命周期钩子）来帮助我们实现这些功能。Vue3中常⻅的DOM操作包括：

使用ref获取DOM元素的引用；

在生命周期钩子中操作DOM元素；

通过v-bind动态修改属性或类；

操作style和class；

事件处理及自定义指令

## 8.1基本用法

Vue3中，使用ref可以访问DOM元素的引用，通过它我们可以直接操作 DOM 元素属性。将ref属性绑定到某个DOM元素后，我们可以通过相应的ref引用对象访问该DOM元素。

![image.png](https://s2.loli.net/2024/10/10/BeE2H9wg6vfpJON.png)

通过ref将inputElement绑定到输入框；在按钮点击事件中，调用inputElement.value.focus()使输入框获得焦点

## 8.2生命钩子中的DOM操作

![image.png](https://s2.loli.net/2024/10/10/nBd39opYMFWLOSC.png)
使用onMounted钩子在组件挂载后操作DOM元素box；修改了box元素的背景颜色。

# 小结

Vue.js支持条件渲染和列表渲染，分别通过v-if和v-for实现动态的内容展示。计算属性是基于依赖自动更新的，性能更高，监听器可以实时监控数据变化，适合处理复杂场景。事件处理使用v-on绑定事件，表单双向绑定通过v-model使数据与视图实时同步，插值语法通过{{ }}可以直接在模板中显示数据，属性绑定则用v-bind动态修改HTML属性。
