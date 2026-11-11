
## 解决方案

### JavaScript 代码：

```javascript
function Second_Greatest_Lowest(arr_num)
{
    arr_num.sort(function(x,y)
        {
        return x-y;
        });
    var uniq = [arr_num[0]];
    var result = [];

    for(var j=1; j < arr_num.length; j++)
    {
        if(arr_num[j-1] !== arr_num[j])
        {
            uniq.push(arr_num[j]);
        }
    }
    result.push(uniq[1],uniq[uniq.length-2]);
    return result.join(',');
}

console.log(Second_Greatest_Lowest([1,2,3,4,5]));
```

## 第7章：对象的秘密生活

在编程语言中，有一套技术将对象用作程序组织的基本思想，它们被称为面向对象编程。本章将进一步解释其概念。

### 封装

面向对象编程的首要意义在于将程序拆分成小块，并确保每一块管理自己的部分。类似程序的多个片段通过接口相互通信，接口是一组受限的函数或绑定，它们在更高层次上提供基本功能，同时隐藏具体执行过程。用对象来说明这类程序片段，其布局包含一组特定的属性和方法。布局内的属性是公开的，而外部代码是私有的。在注释或文档中定义可访问的布局。它经常在属性名开头使用下划线（_）字符来表示私有属性。同时，将布局与执行分离称为封装。

### 方法

方法是持有函数值的属性。

```javascript
let rabbit = {};
rabbit.speak = function(line) {
  console.log(`The rabbit says '${line}'`);
};
rabbit.speak("I'm alive.");
// → The rabbit says 'I'm alive.'
```

当你将函数作为方法调用时，绑定会在其函数体中调用它，并指向它被调用的对象。

```javascript
function speak(line) {
  console.log(`The ${this.type} rabbit says '${line}'`);
}
let whiteRabbit = {type: "white", speak};
let hungryRabbit = {type: "hungry", speak};
whiteRabbit.speak("Oh my whiskers," + "how late it's getting!");
// → The white rabbit says 'Oh my whiskers, how
// late it's getting!'
hungryRabbit.speak("I could use a carrot right now.");
// → The hungry rabbit says 'I could use a carrot right now.'
```

箭头函数不会绑定自己的 this。你可以编写以下代码：

```javascript
function normal() {
  console.log(this.coords.map(n => n / this.length));
}
normal.call({coords: [0, 2, 3], length: 5});
// → [0, 0.4, 0.6]
```

### 原型

留意这一点。

```javascript
let empty = {};
console.log(empty.toString);
// → function toString()...{}
console.log(empty.toString());
// → [object Object]
```

一个属性从空对象中被取出。许多 JavaScript 对象包含一个原型。这是一个用作属性替代来源的对象。因此，那个空对象的原型是继承来的原型，即 Object.prototype。

```javascript
console.log(Object.getPrototypeOf({}) ==
Object.prototype);
// → true
console.log(Object.getPrototypeOf(Object.prototype));
// → null
```

Object.getPrototypeOf 返回一个对象的原型。这个原型产生一些出现在每个对象中的方法，比如 toString，它将对象转换为字符串表示。

许多对象并不以 Object.prototype 作为它们的原型，而是使用另一个对象，该对象产生一组单独的默认属性；

函数从 Function.prototype 获得属性，数组从 Array.prototype 获得属性。

```javascript
console.log(Object.getPrototypeOf(Math.max) ==
Function.prototype);
// → true
console.log(Object.getPrototypeOf([]) ==
Array.prototype);
// → true
```

这种原型对象包含一个原型 Object.prototype，因此它可以间接创建诸如 toString 之类的方法。使用 Object.create 来构建具有特定原型的对象。

```javascript
let protoRabbit = {
  speak(line) {
    console.log(`The ${this.type} rabbit says '${line}'`);
  }
};
let killerRabbit = Object.create(protoRabbit);
killerRabbit.type = "killer";
killerRabbit.speak("SKREEEE!");
// → The killer rabbit says 'SKREEEE!'
```

对象表达式中的 speak(line) 属性产生一个名为 speak 的属性，并将一个函数设为其值。这是一种描述方法的简写方式。“proto”兔子是所有属性的容器。

### 类

JavaScript 的原型系统可以描述为一种称为类的面向对象方法的附属。类描述对象类型的形状、它的属性和方法。原型用于描述属性，使得每个实例共享相似的值，例如方法。如果你想构建一个集合类的实例，创建一个从普通原型接收属性的对象。确保它包含应包含在此类实例中的属性。下面是构造函数。

```javascript
function makeRabbit(type) {
  let rabbit = Object.create(protoRabbit);
  rabbit.type = type;
  return rabbit;
}
```

JavaScript 提供了一种轻松描述此函数的方法。在函数调用前放置 new 关键字。在构造对象期间使用的原型对象，是通过获取构造函数的 prototype 属性得到的。

```javascript
function Rabbit(type) {
  this.type = type;
}
Rabbit.prototype.speak = function(line) {
  console.log(`The ${this.type} rabbit says '${line}'`);
};
let weirdRabbit = new Rabbit("weird");
```

Function.prototype 是构造函数的原型。它的 prototype 属性持有通过它构建的实例所使用的原型。

```javascript
console.log(Object.getPrototypeOf(Rabbit) === Function.prototype);
// → true
console.log(Object.getPrototypeOf(weirdRabbit) === Rabbit.prototype);
// → true
```

### 类记法

JavaScript 类是带有 prototype 属性的构造函数。下面是一个示例：

```javascript
class Rabbit {
  constructor(type) {
    this.type = type;
  }
  speak(line) {
    console.log(`The ${this.type} rabbit says '${line}'`);
  }
}

let killerRabbit = new Rabbit("killer");
let blackRabbit = new Rabbit("black");
```

class 关键字以类声明开始，它使你能够在一个特定位置描述构造函数和一组方法。类声明使方法（持有函数的属性）能够被包含在原型中。当你使用表达式时，它不描述绑定，而是提供构造函数作为值。你可以在表达式中省略类名。

```javascript
let object = new class { getWord() { return "hello"; } };
console.log(object.getWord());
// → hello
```

### 覆盖派生属性

当属性被添加到对象时，无论原型中是否存在该属性，该属性都会添加到对象上。如果原型中有一个已赋值的同名属性，它不会影响该对象。

```javascript
Rabbit.prototype.teeth = "small";
console.log(killerRabbit.teeth);
// → small
killerRabbit.teeth = "long, sharp, and bloody";
console.log(killerRabbit.teeth);
// → long, sharp, and bloody
console.log(blackRabbit.teeth);
// → small
console.log(Rabbit.prototype.teeth);
// → small
```

覆盖属性用于给标准函数和数组原型赋予单独的 toString 方法。

```javascript
console.log(Array.prototype.toString ===
Object.prototype.toString);
// → false
console.log([1, 3].toString());
// → 1,3
```

在数组上调用 toString 会产生类似于对其调用 join(",") 的结果。它在数组包含的值之间放置逗号。如果你对数组调用 Object.prototype.toString，它会提供一个单独的字符串。

```javascript
console.log(Object.prototype.toString.call([1, 3]));
// → [object Array]
```

### 映射

映射是一种将值与另一个值连接起来的数据布局。如果你想将名字映射到年龄，可以这样编写代码：

```javascript
let ages = {
  Boris: 39,
  Liang: 22,
  Júlia: 62
};
console.log(`Júlia is ${ages["Júlia"]}`);
// → Júlia is 62
console.log("Is Jack's age known?", "Jack" in ages);
// → Is Jack's age known? false
console.log("Is toString's age known?", "toString" in ages);
// → Is toString's age known? true
```

对象属性名应使用字符串。如果你想要一个键不能转换为字符串的映射，请不要使用对象作为映射。JavaScript 包含一个名为 Map 的类。它保存映射并允许不同类型的键。

```javascript
let ages = new Map();
ages.set("Boris", 39);
ages.set("Liang", 22);
ages.set("Júlia", 62);
console.log(`Júlia is ${ages.get("Júlia")}`);
// → Júlia is 62
```

