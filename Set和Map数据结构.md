## **Set和Map数据结构**

### 一、Set
> 它类似于数组，但是成员的值都是唯一的，没有重复的值。Set 本身是一个构造函数，用来生成 Set 数据结构。

```javascript
const s = new Set();

[2, 3, 5, 4, 5, 2, 2].forEach(x => s.add(x));

for (let i of s) {
  console.log(i);
}
// 2 3 5 4
```

Set 函数可以接受一个数组（或类似数组的对象）作为参数，用来初始化。

```javascript
/ 例一
const set = new Set([1, 2, 3, 4, 4]);
[...set]
// [1, 2, 3, 4]

// 例二
const items = new Set([1, 2, 3, 4, 5, 5, 5, 5]);
items.size // 5

// 例三
function divs () {
  return [...document.querySelectorAll('div')];
}

const set = new Set(divs());
set.size // 56

// 类似于
divs().forEach(div => set.add(div));
set.size // 56
```

去除数组重复成员的方法。

```javascript
// 去除数组的重复成员
[...new Set(array)]
```

### 二、Set 实例的属性和方法
> * 属性
>	* Set.prototype.constructor：构造函数，默认就是Set函数。
>	* Set.prototype.size：返回Set实例的成员总数。
> * 方法
>	* add(value)：添加某个值，返回Set结构本身。
>	* delete(value)：删除某个值，返回一个布尔值，表示删除是否成功。
>	* has(value)：返回一个布尔值，表示该值是否为Set的成员。
>	* clear()：清除所有成员，没有返回值。

### 三、遍历操作
> * keys()：返回键名的遍历器
> * values()：返回键值的遍历器
> * entries()：返回键值对的遍历器
> * forEach()：使用回调函数遍历每个成员

```javascript
let set = new Set(['red', 'green', 'blue']);

for (let item of set.keys()) {
  console.log(item);
}
// red
// green
// blue

for (let item of set.values()) {
  console.log(item);
}
// red
// green
// blue

for (let item of set.entries()) {
  console.log(item);
}
// ["red", "red"]
// ["green", "green"]
// ["blue", "blue"]

let set = new Set([1, 2, 3]);
set.forEach((value, key) => console.log(value * 2) )
// 2
// 4
// 6

let set = new Set([1, 2, 3]);
set = new Set([...set].map(x => x * 2));
// 返回Set结构：{2, 4, 6}

let set = new Set([1, 2, 3, 4, 5]);
set = new Set([...set].filter(x => (x % 2) == 0));
// 返回Set结构：{2, 4}

let arr = [3, 5, 2, 2, 5, 5];
let unique = [...new Set(arr)];
// [3, 5, 2]
```

### 四、Map
> 它类似于对象，也是键值对的集合，但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键。

```javascript
const map = new Map([
  ['name', '张三'],
  ['title', 'Author']
]);

map.size // 2
map.has('name') // true
map.get('name') // "张三"
map.has('title') // true
map.get('title') // "Author"
```

### 五、Map 实例的属性和方法
> * 属性
>	* Map.prototype.constructor：构造函数，默认就是Map函数。
>	* Map.prototype.size：返回Map实例的成员总数。
> * 方法
>	* set(key, value)：set方法设置键名key对应的键值为value，然后返回整个 Map 结构。如果key已经有值，则键值会被更新，否则就新生成该键。可以采用链式写法。
>	* get(key)：get方法读取key对应的键值，如果找不到key，返回undefined。
>	* has(key)：has方法返回一个布尔值，表示某个键是否在当前 Map 对象之中。
>	* delete(key)：delete方法删除某个键，返回true。如果删除失败，返回false。
>	* clear(): clear方法清除所有成员，没有返回值。

### 六、遍历操作
和 Set 一样
