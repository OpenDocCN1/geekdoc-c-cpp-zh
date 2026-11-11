
```javascript
y: radius * Math.sin(angle) };
}
console.log(randomPointOnCircle(2));
// → {x: 0.3667, y: 1.966}
```

Math.random 函数在你每次调用时都会返回一个介于 0 和 1 之间的新伪随机数。

```javascript
console.log(Math.random());
// → 0.36993729369714856
```

```javascript
console.log(Math.random());
// → 0.727367032552138
console.log(Math.random());
// → 0.40180766698904335
```

当你需要整数随机数而不是小数随机数时，可以对 Math.random 的结果使用 Math.floor。

```javascript
console.log(Math.floor(Math.random() * 10));
// → 2
```

这个随机数乘以 10，得到一个大于等于 0 且小于 10 的数。因为 Math.floor 向下取整，所以输出将是 0 到 9 中的任意数字。Math 对象包含几个函数，例如 Math.ceil（向上取整为整数）、Math.round（四舍五入到最接近的整数）和 Math.abs（返回一个数的绝对值）。

## 解构

让我们稍微使用一下 phi 函数。

```javascript
function phi(table) {
  return (table[3] * table[0] - table[2] * table[1]) /
    Math.sqrt((table[2] + table[3]) *
              (table[0] + table[1]) *
              (table[1] + table[3]) *
              (table[0] + table[2]));
}
```

这个函数难以阅读的原因之一是，有一个绑定指向数组，但我们想要的是数组元素的绑定，也就是 let n00 = table[0] 等等。幸运的是，在 JavaScript 中有更好的方法来实现这一点。

```javascript
function phi([n00, n01, n10, n11]) {
  return (n11 * n00 - n10 * n01) /
    Math.sqrt((n10 + n11) * (n00 + n01) *
              (n01 + n11) * (n00 + n10));
}
```

这也适用于用 let、var 或 const 创建的绑定。如果你知道要绑定的值是一个数组，就可以使用方括号查看该值内部并绑定其内容。对对象使用同样的思路，只是用花括号代替方括号。

```javascript
let {name} = {name: "Faraji", age: 23};
console.log(name);
// → Faraji
```

## JSON

JSON 代表 JavaScript Object Notation（JavaScript 对象表示法），在 Web 上用作数据存储和通信格式。JSON 在书写数组和对象的方式上与 JavaScript 非常相似，尽管存在一些限制。它的属性名必须用双引号括起来，并且只允许简单的数据表达式——不允许绑定、函数调用或注释。

下面是一个用 JSON 数据表示的日记条目示例：

```json
{
  "squirrel": false,
  "events": ["work", "touched tree", "pizza", "running"]
}
```

JavaScript 提供了 JSON.stringify 和 JSON.parse 函数，用于在此格式与其他格式之间转换数据。JSON.stringify 接受一个 JavaScript 值并返回一个 JSON 编码的字符串，而 JSON.parse 接受一个字符串并将其转换回它所编码的值。

```javascript
let string = JSON.stringify({squirrel: false,
events: ["weekend"]});
console.log(string);
// → {"squirrel":false,"events":["weekend"]}
console.log(JSON.parse(string).events);
// → ["weekend"]
```

## 反转数组

数组有一个 reverse 方法，用于通过反转元素出现的顺序来改变数组。

## 总结

本章我们介绍了对象和数组，它们提供了将各种值组合成单个值的方法。形象地说，这让你可以把几个相关的项目放进一个袋子里随身携带，而不是用双臂搂住每个单独的项目并试图分别拿住它们。

JavaScript 中的大多数值都有属性，例外是 undefined 和 null。你可以用 value.prop 或 value["prop"] 访问属性。你可以使用名称在对象上存储一组已定义的属性。另一方面，数组包含数量不定的相似值，并使用数字（从 0 开始）作为属性名。数组有一些内置属性，例如 length 和若干方法。方法是存在于属性中的函数，并作用于它们作为其属性的值。你可以用一种特殊的 for 循环遍历数组——`for (let element of array)`。

## 练习

编写一个 JavaScript 函数来获取数组中的第一个项目。传入参数 'n' 将返回数组的前 'n' 个元素。

数据：

```javascript
console.log(array_Clone([1, 2, 4, 0]));
console.log(array_Clone([1, 2, [4, 0]]));
```

```text
[1, 2, 4, 0]
[1, 2, [4, 0]]
```

## 解答

```javascript
};

console.log(first([7, 9, 0, -2]));
console.log(first([],3));
console.log(first([7, 9, 0, -2],3));
console.log(first([7, 9, 0, -2],6));
console.log(first([7, 9, 0, -2],-3));
```

## 第6章：高阶函数

大型程序需要时间开发，并且会产生大量让 bug 藏身的空间，这反过来又使它们难以被发现。下面是两个大型程序的示例：

第一个是自包含的，程序有六行。

```javascript
let total = 0, count = 1;
while (count <= 10) {
  total += count;
  count += 1;
}
console.log(total);
```

第二个依赖两个外部函数，其语句只有一行。

```javascript
console.log(sum(range(1, 10)));
```

### 抽象

在编程语境中，这类词汇通常被称为抽象。抽象隐藏细节，并让我们能够在更高层次上讨论问题。让我们比较两份豌豆汤食谱。

第一份：

每人将 1 杯干豌豆放入容器中。加入足够的水没过豌豆，浸泡约 12 小时。将它们从水中取出，放入烹饪锅中，每人加 4 杯水。煮沸约两小时。每人半个洋葱，用刀切片后加入豌豆中，再煮 10 分钟。

然后是第二份食谱：

每人：半个洋葱、一根芹菜、1 杯干豌豆瓣和一根胡萝卜。将豌豆在水中浸泡约 12 小时。用 4 杯水煮约 2 小时，然后切好蔬菜并加入。煮 10 分钟。

计算机以盲目的、低层的方式一项一项执行任务；抽象让我们能够使用高层概念工作。

### 抽象重复

普通函数是构建抽象的好方法。程序常常需要将某个特定动作重复特定次数。你可以用这样的循环来完成：

```javascript
for (let i = 0; i < 10; i++) {
  console.log(i);
}
```

这里我们编写一个调用 console.log n 次的函数。

```javascript
function repeatLog(n) {
  for (let i = 0; i < n; i++) {
    console.log(i);
  }
}
```

如果你想执行记录数字之外的任务，可以将一个动作作为函数值传入。

```javascript
function repeat(n, action) {
  for (let i = 0; i < n; i++) {
    action(i);
  }
}

repeat(3, console.log);
// → 0
// → 1
// → 2
```

有时你不需要传入一个预定义的函数来在循环中重复；可以改为创建一个函数值：

```javascript
let labels = [];
repeat(5, i => {
  labels.push(`Unit ${i + 1}`);
});
console.log(labels);
// → ["Unit 1", "Unit 2", "Unit 3", "Unit 4", "Unit 5"]
```

这种方法看起来类似于循环——它描述了循环的种类，然后提供一个循环体。不过，循环体是作为函数值写在 repeat 调用的括号中的。

### 高阶函数

高阶函数是作用于其他函数的函数，要么将它们作为参数，要么返回它们。这类函数使我们能够对动作进行抽象。例如，你可以有一个生成函数的函数：

```javascript
function greaterThan(n) {
  return m => m > n;
}

let greaterThan10 = greaterThan(10);
console.log(greaterThan10(11));
// → true
```

你也可以有转换其他函数的函数。
