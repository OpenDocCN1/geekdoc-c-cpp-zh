

## 定义属性

回顾第 1 章，有两种基本方法可以创建自己的对象：使用 Object 构造函数和使用对象字面量。例如：

```
var person1 = {
  name: "Nicholas"
};

var person2 = new Object();
person2.name = "Nicholas";

① person1.age = "Redacted";
person2.age = "Redacted";

② person1.name = "Greg";
person2.name = "Michael";
```

person1 和 person2 都是具有 name 属性的对象。稍后在示例中，两个对象都被赋予了 age 属性 ①。你可以在对象定义后立即执行此操作，也可以在 much later。 除非另有指定，否则你创建的对象始终可以自由修改（更多内容请参见第 45 页的“防止对象修改”）。此示例的最后一部分更改了每个对象中 name 的值 ②；属性值也可以随时更改。

当向对象首次添加属性时，JavaScript 会在对象上使用一个名为 [[Put]] 的内部方法。[[Put]] 方法在对象中创建存储属性的位置。你可以将此与首次向哈希表添加键进行比较。此操作指定不仅仅是初始值，还指定属性的一些属性。因此，在前面的示例中，当 name 和 age 属性首次在每个对象上定义时，就会为每个属性调用 [[Put]] 方法。

调用 [[Put]] 的结果是在对象上创建一个自身属性。自身属性 simply 表示该特定对象实例拥有该属性。该属性直接存储在实例上，并且对该属性的所有操作都必须通过该对象执行。

> 注意 自身属性与原型属性不同，原型属性将在第 4 章中讨论。

当为现有属性分配新值时，会发生一个名为 [[Set]] 的单独操作。此操作用新值替换属性的当前值。在前面的示例中，将 name 设置为第二个值会导致对 [[Set]] 的调用。图 3-1 逐步展示了 person1 的 name 和 age 属性发生变化时幕后发生的情况。

![](img/dcf53336af93733d4dab8829d31ceb8e_53_0.png)

图 3-1：添加和更改对象的属性

在图表的第一部分，使用对象字面量创建 person1 对象。这会隐式地对 name 属性执行 [[Put]]。将值分配给 person1.age 会对 age 属性执行 [[Put]]。然而，将 person1.name 设置为新值 ("Greg") 会对 name 属性执行 [[Set]] 操作，覆盖现有的属性值。

## 检测属性

由于属性可以随时添加，因此有时需要检查对象中是否存在属性。新 JavaScript 开发人员经常错误地使用以下模式来检测属性是否存在：

```
// unreliable
if (person1.age) {
    // do something with age
}
```

这种模式的问题在于 JavaScript 的类型强制转换如何影响结果。if 条件在值是 truthy（对象、非空字符串、非零数字或 true）时求值为 true，在值是 falsy（null、undefined、0、false、NaN 或空字符串）时求值为 false。由于对象属性可以包含这些 falsy 值，因此示例代码可能会产生假阴性。例如，如果 person1.age 为 0，则 if 条件将不满足，即使属性存在。更可靠地测试属性是否存在的方法是使用 in 运算符。

in 运算符会在特定对象中查找具有给定名称的属性，如果找到则返回 true。实际上，in 运算符检查给定键是否存在于哈希表中。例如，以下是使用 in 检查 person1 对象中的一些属性时会发生的情况：

```
console.log("name" in person1);    // true
console.log("age" in person1);      // true
console.log("title" in person1);    // false
```

请记住，方法只是引用函数的属性，因此你可以用相同的方式检查方法的存在。以下代码向 person1 添加了一个新函数 sayName()，并使用 in 确认该函数的存在。

```
var person1 = {
    name: "Nicholas",
    sayName: function() {
        console.log(this.name);
    }
};

console.log("sayName" in person1);  // true
```

在大多数情况下，in 运算符是确定属性是否存在于对象中的最佳方法。它还有一个额外的好处，即不会评估属性的值，这在评估可能导致性能问题或错误时可能很重要。

然而，在某些情况下，你可能只想检查属性是否存在且为自身属性。in 运算符会检查自身属性和原型属性，因此你需要采用不同的方法。进入 hasOwnProperty() 方法，该方法存在于所有对象上，并且仅在给定属性存在且为自身属性时才返回 true。例如，以下代码比较了在 person1 中的不同属性上使用 in 与 hasOwnProperty() 的结果：

```
var person1 = {
    name: "Nicholas",
    sayName: function() {
        console.log(this.name);
    }
};

console.log("name" in person1);                     // true
console.log(person1.hasOwnProperty("name"));        // true

console.log("toString" in person1);                 // true
console.log(person1.hasOwnProperty("toString"));    // false
```

在此示例中，name 是 person1 的自身属性，因此 in 运算符和 hasOwnProperty() 都返回 true。然而，toString() 方法是存在于所有对象上的原型属性。in 运算符对 toString() 返回 true，但 hasOwnProperty() 返回 false ①。这是将在第 4 章中进一步讨论的重要区别。

## 删除属性

正如属性可以随时添加到对象中一样，它们也可以被删除。仅仅将属性设置为 null 并不会真正从对象中完全删除该属性。这样的操作会调用 [[Set]] 并将值设置为 null，正如你在本章前面看到的那样，这只会替换属性的值。你需要使用 delete 运算符才能完全从对象中删除属性。

delete 运算符作用于单个对象属性并调用名为 [[Delete]] 的内部操作。你可以将此操作视为从哈希表中删除键/值对。当 delete 运算符成功时，它会返回 true。（有些属性不能被删除，这将在本章后面更详细地讨论。）例如，以下列表显示了 delete 运算符的工作方式：

```
var person1 = {
  name: "Nicholas"
};

console.log("name" in person1);    // true

delete person1.name;                // true - not output
console.log("name" in person1);    // false
console.log(person1.name);          // undefined
```

在此示例中，name 属性已从 person1 中删除。操作完成后，in 运算符返回 false。此外，请注意，尝试访问不存在的属性只会返回 undefined ①。图 3-2 显示了 delete 如何影响对象。

![](img/dcf53336af93733d4dab8829d31ceb8e_55_0.png)

图 3-2：当你删除 name 属性时，它会完全从 person1 中消失。

## 枚举

默认情况下，你添加到对象的属性都是可枚举的，这意味着你可以使用 for-in 循环迭代它们。可枚举属性的内部 [[Enumerable]] 属性设置为 true。for-in 循环枚举对象上的所有可枚举属性，并将属性名称分配给变量。例如，以下循环输出对象的属性名称和值：

```
var property;

for (property in object) {
    console.log("Name: " + property);
    console.log("Value: " + object[property]);
}
```

每次通过 for-in 循环，property 变量都会填充对象上的下一个可枚举属性，直到使用完所有此类属性。此时，循环结束，代码执行继续。此示例使用方括号表示法检索对象属性的值并将其输出到控制台，这是 JavaScript 中方括号表示法的主要用例之一。

如果你只需要一个稍后在程序中使用的对象属性列表，ECMAScript 5 引入了 Object.keys() 方法来检索可枚举属性名称的数组，如下所示：

```
var properties = Object.keys(object);

// if you want to mimic for-in behavior
var i, len;

for (i=0, len=properties.length; i < len; i++){
    console.log("Name: " + properties[i]);
    console.log("Value: " + object[properties[i]]);
}
```

此示例使用 Object.keys() 从对象中检索可枚举属性 ①。然后使用 for 循环迭代属性并输出名称和值。通常，你会在想要对属性名称数组进行操作时使用 Object.keys()，而在不需要数组时使用 for-in。

> 注意 for-in 循环返回的可枚举属性与 Object.keys() 返回的属性之间存在差异。for-in 循环还会枚举原型属性，而 Object.keys() 只返回自身（实例）属性。原型和自身属性之间的差异将在第 4 章中讨论。

