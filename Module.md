## **Module**

### 概述
>在 ES6 之前，社区制定了一些模块加载方案，最主要的有 CommonJS 和 AMD 两种。前者用于服务器，后者用于浏览器。ES6 在语言标准的层面上，实现了模块功能，ES6 模块的设计思想，是尽量的静态化，使得编译时就能确定模块的依赖关系，以及输入和输出的变量。CommonJS 和 AMD 模块，都只能在运行时确定这些东西。比如，CommonJS 模块就是对象，输入时必须查找对象属性。

```javascript
// CommonJS模块
let { stat, exists, readFile } = require('fs');

// 等同于
let _fs = require('fs');
let stat = _fs.stat;
let exists = _fs.exists;
let readfile = _fs.readfile;
```
上面代码的实质是整体加载fs模块（即加载fs的所有方法），生成一个对象（_fs），然后再从这个对象上面读取3个方法。这种加载称为“运行时加载”，因为只有运行时才能得到这个对象，导致完全没办法在编译时做“静态优化”。

>ES6 模块不是对象，而是通过export命令显式指定输出的代码，再通过import命令输入。

```javascript
// ES6模块
import { stat, exists, readFile } from 'fs';
```
上面代码的实质是从fs模块加载3个方法，其他方法不加载。这种加载称为“编译时加载”或者静态加载，即 ES6 可以在编译时就完成模块加载，效率要比 CommonJS 模块的加载方式高。

### 严格模式
>ES6 的模块自动采用严格模式，不管你有没有在模块头部加上"use strict";。

严格模式主要有以下限制:
	* 变量必须声明后再使用
	* 函数的参数不能有同名属性，否则报错
	* 不能使用with语句
	* 不能对只读属性赋值，否则报错
	* 不能使用前缀0表示八进制数，否则报错
	* 不能删除不可删除的属性，否则报错
	* 不能删除变量delete prop，会报错，只能删除属性delete global[prop]
	* eval不会在它的外层作用域引入变量
	* eval和arguments不能被重新赋值
	* arguments不会自动反映函数参数的变化
	* 不能使用arguments.callee
	* 不能使用arguments.caller
	* 禁止this指向全局对象
	* 不能使用fn.caller和fn.arguments获取函数调用的堆栈
	* 增加了保留字（比如protected、static和interface）

### export 命令
>export命令用于规定模块的对外接口

```javascript
// 输出变量
export let firstName = 'Michael';
export let lastName = 'Jackson';
export let year = 1958;

//或者简写
let firstName = 'Michael';
let lastName = 'Jackson';
let year = 1958;

export {firstName, lastName, year};

//输出函数或类（class）
export function multiply(x, y) {
  return x * y;
};
```

### import 命令
>import命令用于输入其他模块提供的功能，import命令具有提升效果，会提升到整个模块的头部，首先执行

```javascript
import {firstName, lastName, year} from './index';

function setName(element) {
  element.textContent = firstName + ' ' + lastName;
}
```

**as关键字**
```javascript
//为输入的变量重新取一个名字
import { lastName as surname } from './index';

//模块整体加载
import * as circle from './circle'
```

### export default 命令
>为模块指定默认输出

```javascript
// export-default.js
export default function () {
  console.log('foo');
}

// import-default.js
import customName from './export-default';
customName(); // 'foo'
```

### 栗子
* 一个 vuex 模块（module）实例
```javascript
//com.js
import * as types from '../types'

const state = {
    showLoading: false,
}

const actions = {
    setShowLoading({ commit }, status) {
        commit(types.COM_SHOW_LOADING, status)
    }
}

const getters = {
    showLoading: state => state.showLoading,
}


const mutations = {
    [types.COM_SHOW_LOADING](state, status) {
        state.showLoading = status
    },
}


export default {
    state,
    actions,
    getters,
    mutations
}

//serach.vue
import { mapGetters } from 'vuex'

computed: {
	//mapGetters(map: Array<string> | Object): Object,创建组件的计算属性返回 getter 的返回值
	//使用对象展开运算符将 getters 混入 computed 对象中
    ...mapGetters([
        'showLoading'
	])
},
```