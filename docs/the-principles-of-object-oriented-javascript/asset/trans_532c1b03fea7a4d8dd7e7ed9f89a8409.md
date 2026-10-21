
## 摘要

将 JavaScript 对象视为哈希映射会很有帮助，其中属性只是键/值对。你可以使用点表示法或带字符串标识符的方括号表示法来访问对象属性。你可以随时通过给属性赋值来添加属性，也可以随时使用 delete 运算符删除属性。你始终可以使用 in 运算符，在属性名和对象上检查某个属性是否存在。如果该属性是自有属性，你还可以使用每个对象上都存在的 hasOwnProperty() 方法。默认情况下，所有对象属性都是可枚举的，这意味着它们会出现在 for-in 循环中，或者可以通过 Object.keys() 获取。

属性有两种类型：数据属性和访问器属性。数据属性是值的占位符，你可以对它们进行读取和写入。当数据属性保存了一个函数值时，该属性被视为对象的方法。与数据属性不同，访问器属性本身不存储值；它们结合 getter 和 setter 来执行特定操作。你可以直接使用对象字面量表示法来创建数据属性和访问器属性。

所有属性都有多个相关联的特性。这些特性定义了属性如何工作。数据属性和访问器属性都有 [[Enumerable]] 和 [[Configurable]] 特性。数据属性还有 [[Writable]] 和 [[Value]] 特性，而访问器属性则有 [[Get]] 和 [[Set]] 特性。默认情况下，所有属性的 [[Enumerable]] 和 [[Configurable]] 都设置为 true，数据属性的 [[Writable]] 也设置为 true。你可以使用 Object.defineProperty() 或 Object.defineProperties() 来更改这些特性。也可以使用 Object.getOwnPropertyDescriptor() 来检索这些特性。

当你希望以某种方式锁定对象的属性时，有三种不同的方法可以做到。如果你使用 Object.preventExtensions()，对象将不再允许添加属性。你也可以使用 Object.seal() 方法创建一个密封对象，这会使该对象不可扩展，并使其属性不可配置。Object.freeze() 方法创建一个冻结对象，这是一个密封对象，且其数据属性不可写。要小心不可扩展对象，并且始终使用严格模式，以便错误地访问对象时会抛出错误。

## 4 构造函数和原型

即使不理解构造函数和原型，你也可能在使用 JavaScript 时走得相当远，但如果没有很好地掌握它们，你就不会真正欣赏这门语言。由于 JavaScript 缺乏类，它借助构造函数和原型为对象带来类似的秩序。但仅仅因为某些模式类似类，并不意味着它们的行为方式相同。在本章中，你将详细探索构造函数和原型，了解 JavaScript 如何使用它们来创建对象。

![](img/dcf53336af93733d4dab8829d31ceb8e_69_0.png)

构造函数只是一个与 new 一起使用来创建对象的函数。到目前为止，你已经见过几个内置的 JavaScript 构造函数，例如 Object、Array 和 Function。构造函数的好处是，使用同一个构造函数创建的对象包含相同的属性和方法。如果你想创建多个相似的对象，你可以创建自己的构造函数，从而创建自己的引用类型。

因为构造函数只是一个函数，所以你可以用相同的方式定义它。唯一的区别是构造函数名应以大写字母开头，以便与其他函数区分。例如，看下面的空 Person 函数：

```
function Person() {
 // intentionally empty
}
```

这个函数是一个构造函数，但它与任何其他函数之间绝对没有语法差异。表明 Person 是构造函数的线索在于名称——第一个字母大写。

定义构造函数后，你就可以开始创建实例，比如下面两个 Person 对象：

```
var person1 = new Person();
var person2 = new Person();
```

当没有参数需要传给构造函数时，你甚至可以省略括号：

```
var person1 = new Person;
var person2 = new Person;
```

即使 Person 构造函数没有显式返回任何内容，person1 和 person2 仍被视为新的 Person 类型的实例。new 运算符会自动创建给定类型的对象并返回它。这也意味着你可以使用 instanceof 运算符来推断对象的类型。下面的代码演示了 instanceof 与新建对象一起使用的效果：

```
console.log(person1 instanceof Person); // true
console.log(person2 instanceof Person); // true
```

因为 person1 和 person2 是使用 Person 构造函数创建的，所以当 instanceof 检查这些对象是否为 Person 类型的实例时，会返回 true。

你还可以使用 constructor 属性来检查实例的类型。每个对象实例都会自动创建一个 constructor 属性，其中包含对创建它的构造函数函数的引用。对于泛型对象（通过对象字面量或 Object 构造函数创建的对象），constructor 被设置为 Object；对于使用自定义构造函数创建的对象，constructor 会指向那个构造函数函数。例如，Person 就是 person1 和 person2 的 constructor 属性：

```
console.log(person1.constructor === Person);    // true
console.log(person2.constructor === Person);    // true
```

在这两种情况下，console.log 函数都会输出 true，因为这两个对象都是使用 Person 构造函数创建的。

即使实例与其构造函数之间存在这种关系，仍建议你使用 instanceof 来检查实例的类型。这是因为 constructor 属性可以被覆盖，因此可能不完全准确。

当然，空的构造函数函数不是很有用。构造函数的全部意义在于轻松创建更多具有相同属性和方法的对象。要做到这一点，只需在构造函数内部把你想添加的任何属性添加到 this 上，如下例所示：

```
function Person(name) {
    this.name = name;
    this.sayName = function() {
        console.log(this.name);
    };
}
```

这个版本的 Person 构造函数接受一个名为 name 的单一命名参数，并将其赋值给 this 对象的 name 属性①。构造函数还向对象添加了一个 sayName() 方法②。this 对象是在你调用构造函数时由 new 自动创建的，它是构造函数类型的实例。（在这种情况下，this 是 Person 的一个实例。）不需要从函数中返回值，因为 new 运算符会产生返回值。

现在你可以使用 Person 构造函数创建具有已初始化 name 属性的对象：

```
var person1 = new Person("Nicholas");
var person2 = new Person("Greg");

console.log(person1.name);          // "Nicholas"
console.log(person2.name);          // "Greg"

person1.sayName();                  // outputs "Nicholas"
person2.sayName();                  // outputs "Greg"
```

每个对象都有自己的 name 属性，所以 sayName() 应该根据你使用它的对象返回不同的值。

注意：你也可以在构造函数内部显式地调用 return。如果返回的值是一个对象，则会返回该对象而不是新创建的对象实例。如果返回的值是一个原始值，则会使用新创建的对象，而返回的值被忽略。

构造函数允许你以一致的方式初始化一个类型的实例，在执行完对象使用前所有必要的属性设置后，对象才能被使用。例如，你也可以在构造函数中使用 Object.defineProperty() 来帮助初始化实例：

```
function Person(name) {

    Object.defineProperty(this, "name", {
        get: function() {
            return name;
        },
        set: function(newName) {
            name = newName;
        },
        enumerable: true,
        configurable: true
    });

    this.sayName = function() {
        console.log(this.name);
    };
}
```

在这个版本的 Person 构造函数中，name 属性是一个访问器属性，它使用 name 参数来存储实际的名称。这是可能的，因为命名参数的行为类似于局部变量。请务必始终使用 new 来调用构造函数；否则，你可能会修改全局对象而不是新创建的对象。考虑下面的代码会发生什么：

```
var person1 = Person("Nicholas");        // note: missing "new"

console.log(person1 instanceof Person);    // false
console.log(typeof person1);                // "undefined"
console.log(name);                          // "Nicholas"
```

当 Person 在没有 new 的情况下作为函数调用时，构造函数内部的 this 值等于全局 this 对象。变量 person1 不包含值，因为 Person 构造函数依赖 new 来提供返回值。没有 new，Person 只是一个没有 return 语句的函数。对 this.name 的赋值实际上创建了一个全局变量。

