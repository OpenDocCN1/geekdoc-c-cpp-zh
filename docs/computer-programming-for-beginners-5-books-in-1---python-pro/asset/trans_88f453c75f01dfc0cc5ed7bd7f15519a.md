

`push` 方法用于将值添加到数组末尾，而 `pop` 方法则正好相反。它会移除数组中的最后一个值并将其返回。这些都是栈操作的通用术语。栈是一种数据结构，允许用户将值压入（push）栈中，并以相反方向弹出（pop），因此最后添加的值最先被移除。

## 对象

你可以将一组日志条目表示为一个数组，但每个条目都需要保存一系列活动，以及一个指定 Jacques 是否变成松鼠的布尔值。我们将其归并为一个值，然后将这些归并后的值放入日志条目数组中。对象类型的值就是任意属性集合。我们将使用花括号作为表达式来创建对象。

```javascript
let day1 = {
  squirrel: false,
  events: ["work", "touched tree", "pizza", "running"]
};
console.log(day1.squirrel);
// → false
console.log(day1.wolf);
// → undefined
day1.wolf = false;
console.log(day1.wolf);
// → false
```

花括号中包含一个由逗号分隔的属性列表。每个属性都有一个名称、一个冒号和一个值。当对象分成多行编写时，请确保缩进良好，因为这样可以提高可读性。属性名如果既不是有效的绑定名称，也不是有效的数字，就应该用引号括起来。

```javascript
let descriptions = {
  work: "Went to work",
  "touched tree": "Touched a tree."
};
```

在 JavaScript 中，花括号有两种不同的用法。它可以放在语句开头，也可以用来开始一个语句块。你可以使用 `=` 运算符为属性表达式赋值。它会替换该属性的值；如果属性不存在，则会创建一个新属性。`delete` 运算符是一元运算符，用于删除对象的属性名。下面是一个示例：

```javascript
let anObject = {left: 1, right: 2};
console.log(anObject.left);
// → 1
delete anObject.left;
console.log(anObject.left);
// → undefined
console.log("left" in anObject);
// → false
console.log("right" in anObject);
// → true
```

二元 `in` 运算符用于确定对象或字符串是否包含某个命名属性。将属性设置为 `undefined` 与删除该属性的主要区别在于：前一种情况下，对象仍然包含该属性；而删除后，对象不再拥有该属性，因此 `in` 返回 false。`Object.keys` 用于确定对象包含哪些属性，并返回一个包含对象属性名的字符串数组。

```javascript
console.log(Object.keys({x: 0, y: 0, c: 2}));
// → ["x", "y", "c"]
```

`Object.assign` 函数用于将属性从一个对象复制到另一个对象。

```javascript
let objectA = {a: 1, b: 2};
Object.assign(objectA, {b: 3, c: 4});
console.log(objectA);
// → {a: 1, b: 3, c: 4}
```

数组是一种特殊的对象，用于保存一系列事物。当你使用 `typeof []` 时，它会返回 `"object"`。下面的示例展示了 Jacques 将日志存储为对象数组的形式。

```javascript
let journal = [
  {events: ["work", "touched tree", "pizza",
    "running", "television"],
    squirrel: false},
  {events: ["work", "ice cream", "cauliflower",
    "lasagna", "touched tree", "brushed teeth"],
    squirrel: false},
  {events: ["weekend", "cycling", "break", "peanuts",
    "beer"],
    squirrel: true},
  /* and so on... */
];
```

## 可变性

我们已经讨论过布尔值、字符串和数字等不同类型的值，它们是不可变的，但你可以组合它们来获得新值。对象与这些值不同，它们允许修改属性；同一个对象值在不同时间可以拥有不同的内容。当存在两个数字 120 和 120 时，它们被认为是相同的；而在将两个引用指向同一个对象与拥有两个包含相同属性的不同对象之间，也存在一个相似的问题。请看下面的代码：

```javascript
let object1 = {value: 10};
let object2 = object1;
let object3 = {value: 10};
console.log(object1 == object2);
// → true
console.log(object1 == object3);
// → false
object1.value = 15;
console.log(object2.value);
// → 15
console.log(object3.value);
// → 10
```

`object1` 和 `object2` 这两个绑定指向同一个对象，因此修改 `object1` 会影响 `object2` 的值，它们本质上相同。绑定 `object3` 指向另一个与 `object1` 具有相似属性的独立对象，但标识不同。绑定可以是常量，也可以是变量，但这不会影响它们所指向的值。对象的 `const` 绑定不能被重新赋值，并且始终指向同一个对象；可以改变的是对象的内容。

```javascript
const score = {visitors: 0, home: 0};
// This is okay
score.visitors = 1;
// This isn't allowed
score = {visitors: 1, home: 1};
```

当 JavaScript 的 `==` 运算符用于比较对象时，它会根据对象的标识进行判断。如果两个对象是同一个值，则返回 true；比较不同的对象将返回 false，即使它们的属性相似。

## 狼人的日志

于是，你启动 JavaScript 解释器，并创建记录日志所需的环境。

```javascript
let journal = [];
function addEntry(events, squirrel) {
  journal.push({events, squirrel});
}
```

它不是显式声明 `events` 这样的属性，而是直接提供属性名。于是，每天晚上 10 点，或偶尔在第二天早上，从书柜顶层爬下来后，你记录下每天的情况。

```javascript
addEntry(["work", "touched tree", "pizza", "running", "television"], false);
addEntry(["work", "ice cream", "cauliflower", "lasagna", "touched tree", "brushed teeth"], false);
addEntry(["weekend", "cycling", "break", "peanuts", "beer"], true);
```

相关性是衡量统计变量之间依赖关系的指标，取值范围为 -1 到 1。不相关的变量称为零相关。相关性为 1 表示两者相关；负相关则意味着变量之间完全相关，但方向相反：一个为真，另一个为假。要计算两个布尔值之间的相关性，可以使用 phi 系数（φ）。该公式的输入是一个频率表，其中记录了观测到的各种变量组合的次数。公式的输出是一个介于 -1 和 1 之间的数字。这是对相关性的最佳定义。

让我们以吃披萨这一事件为例，把它放入一个频率表中；表中的每个数字都代表我们在测量中观察到该组合的次数。我们将这个表命名为 n，并使用下面的公式计算 φ：

```text
φ =
(n11 n00 − n10 n01) / √(n1• n0• n•1 n•0)
```

记号 n01 表示第一个变量为假（0）且第二个变量为真（1）时的测量次数。在披萨表中，n01 为 9。

值 n1• 表示所有第一个变量为真的测量次数之和，在表格示例中为 5。同样，n•0 表示第二个变量为假的测量次数。在披萨表中，分子为 1×76−4×9 = 40，分母为 5×85×10×80 的平方根，即 √340000。结果为 φ ≈ 0.069，非常小。因此，吃披萨对变身没有影响。

## 计算相关性

JavaScript 可以用四元素数组（[76, 9, 4, 1]）表示二乘二表格。也可以使用其他表示方式，例如一个包含两个二元素数组的数组（[[76, 9], [4, 1]]），或者一个包含 "11" 和 "01" 等属性名的对象；后一种表示方式会让访问表格的表达式变得简短。我们将数组的索引解释为两位二进制数，其中最高位表示松鼠变量，最低位表示事件。例如，二进制数 10 表示“Jacques 确实变成了松鼠”但事件没有发生的情况。这种情况出现了四次；二进制 10 对应十进制 2，因此该计数存储在数组索引 2 处。下面的函数根据数组计算 φ 系数：

```javascript
function phi(table) {
  return (table[3] * table[0] - table[2] * table[1]) /
    Math.sqrt((table[2] + table[3]) *
    (table[0] + table[1]) *
    (table[1] + table[3]) *
    (table[0] + table[2]));
}

console.log(phi([76, 9, 4, 1]));
// → 0.068599434
```

这个表格需要两个字段来获取像 n1• 这样的计数，因为行总数和列总数是间接存储在我们的数据布局中的。如果你想提取某个特定事件的二乘二表格，就必须遍历所有条目，并计算该事件与松鼠变身之间各种组合出现的次数。

```javascript
function tableFor(event, journal) {
  let table = [0, 0, 0, 0];
  for (let i = 0; i < journal.length; i++) {
    let entry = journal[i], index = 0;
    if (entry.events.includes(event)) index += 1;
    if (entry.squirrel) index += 2;
    table[index] += 1;
  }
  return table;
}
```

