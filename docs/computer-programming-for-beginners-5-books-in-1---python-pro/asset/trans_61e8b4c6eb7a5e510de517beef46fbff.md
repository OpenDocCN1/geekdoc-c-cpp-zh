
```
// → 8
```

从 exec 返回的对象包含一个 index 属性，它确定成功匹配在字符串中开始的位置。下面是所需的数字序列：

```
console.log("one two 100".match(/\d+/));
// → ["100"]
```

当正则表达式包含用括号分组的子表达式时，与这些组匹配的文本也会出现在数组中。整个匹配是第一个元素，接下来是第一个组匹配的部分，然后是后续组，依此类推。

```
let quotedText = /'([^']*)'/;
console.log(quotedText.exec("she said 'hello'"));
// → ["'hello'", "hello"]
```

当一个组最终没有匹配时（例如，如果它后面跟着问号），它会输出 undefined。当一个组匹配多次时，只有最后一次匹配会出现在数组中。

```
console.log(/(bad)(ly)?/.exec("bad"));
// → ["bad", "bad", undefined]
console.log(/(\d)+/.exec("123"));
// → ["123", "3"]
```

## Date 类

JavaScript 有一个表示日期的标准类；它叫作 Date。如果你想使用 new 创建日期对象，可以不带参数调用它来获取当前时间和日期。

```
console.log(new Date());
// → Mon Nov 11 2018 16:19:11 GMT+0100 (CET)
```

你也可以为特定时间构建对象。

```
console.log(new Date(2008, 11, 8));
// → Mon Dec 08 2008 00:00:00 GMT+0100 (CET)
console.log(new Date(2008, 11, 1, 9, 12, 59, 59, 999));
// → Mon Dec 01 2008 09:12:59 GMT+0100 (CET)
```

你应遵循 JavaScript 的日期命名约定：月份数字从零开始（因此，十二月是 11），日期数字从 1 开始。

小时、分钟、秒和毫秒参数是可选的，未指定时默认为零。时间戳以 UTC 时区中的毫秒数存储，遵循“Unix 时间”设定的约定。

```
console.log(new Date(2013, 11, 14).getTime());
// → 1386975600000
console.log(new Date(1386975600000));
// → Sat Dec 14 2013 00:00:00 GMT+0100 (CET)
```

当 Date 构造函数只接收一个参数时，该参数会被视为毫秒数。你可以通过创建一个新的 Date 对象并在其上调用 getTime，或使用 Date.now 函数，来确定当前毫秒数。Date 对象提供 getDate、getHours、getFullYear、getMonth、getMinutes 和 getSeconds 等方法来获取其组成部分。

```
function getDate(string) {
  let [_, month, day, year] =
    /^(\d{1,2})-(\d{1,2})-(\d{4})$/.exec(string);
  return new Date(year, month - 1, day);
}
console.log(getDate("1-30-2003"));
// → Thu Jan 30 2003 00:00:00 GMT+0100 (CET)
```

## 单词与字符串边界

你可以通过添加标记 ^ 和 $ 来确保匹配覆盖整个字符串。脱字符匹配输入字符串的开头，而美元符号匹配结尾。因此，/^\d+$/ 匹配完全由一个或多个数字组成的字符串，/^!/ 匹配任何以感叹号开头的字符串，而 /x^/ 不匹配任何字符串。如果你希望匹配在单词边界开始和结束，请使用标记 \b。单词边界是单词字符（\w）在一侧、非单词字符在另一侧的位置。

```
console.log(/cat/.test("concatenate"));
// → true
console.log(/\bcat\b/.test("concatenate"));
// → false
```

## 选择模式

如果你想知道一段文本是否包含一个数字，后面跟着 chicken、pig 或 cow 中的一个单词，你可以编写三个正则表达式并测试它们。我们使用竖线字符（|）表示其左侧模式和右侧模式之间的选择：

```
let animalCount = /\b\d+ (pig|cow|chicken)s?\b/;
console.log(animalCount.test("15 pigs"));
// → true
console.log(animalCount.test("15 pigchickens"));
// → false
```

## replace 方法

字符串值有一个 replace 方法，可用于将字符串的一部分替换为另一个字符串。

```
console.log("papa".replace("p", "m"));
// → mapa
```

第一个参数也可以是正则表达式，并且会替换正则表达式的第一个匹配项。如果你向表达式添加 g 选项（表示 global），则字符串中的每个匹配项都会被替换，而不仅仅是第一个。

```
console.log("Borobudur".replace(/[ou]/, "a"));
// → Barobudur
console.log("Borobudur".replace(/[ou]/g, "a"));
// → Barabadar
```

将正则表达式与 replace 结合使用的真正强大之处在于，我们可以在替换字符串中引用匹配的组。例如，你有一个包含人名的大字符串，每行一个，格式为 Lastname, Firstname。你可以使用以下代码交换这些名字、移除逗号，并得到 Firstname Lastname 格式：

```
console.log(
"Liskov, Barbara\nMcCarthy, John\nWadler, Philip"
.replace(/(\w+), (\w+)/g, "$2 $1"));
// → Barbara Liskov
// John McCarthy
// Philip Wadler
```

替换字符串中的 $1 和 $2 指模式中的带括号的组。$1 被替换为与第一个组匹配的文本，$2 被第二个组匹配的文本替换，依此类推，直到 $9。整个匹配可以用 $& 引用。你可以传递一个函数而不是字符串作为第二个参数。对于每次替换，该函数会以匹配的组作为参数被调用，其返回值会被插入到新字符串中。

```
let s = "the cia and fbi";
console.log(s.replace(/\b(fbi|cia)\b/g,
str => str.toUpperCase()));
// → the CIA and FBI
```

这里有一个更有趣的例子：

```
let stock = "1 lemon, 2 cabbages, and 101 eggs";
function minusOne(match, amount, unit) {
  amount = Number(amount) - 1;
  if (amount === 1) { // only one left, remove the 's'
    unit = unit.slice(0, unit.length - 1);
  } else if (amount === 0) {
    amount = "no";
  }
  return amount + " " + unit;
}
console.log(stock.replace(/(\d+) (\w+)/g, minusOne));
// → no lemon, 1 cabbage, and 100 eggs
```

## 贪婪

你可以使用 replace 编写一个函数，从一段 JavaScript 代码中删除所有注释。

```
function stripComments(code) {
  return code.replace(/\/\/.*|\/\*[^]*\*\//g, "");
}
console.log(stripComments("1 + /* 2 */3"));
// → 1 + 3
console.log(stripComments("x = 10; // ten!"));
// → x = 10;
console.log(stripComments("1 /* a */+/* b */ 1"));
// → 1 1
```

or 运算符之前的部分匹配两个斜杠字符，后面跟着任意数量的非换行字符。使用 [^] 匹配任何字符，包括换行符。重复运算符（+、* 和 {}）是贪婪的，意味着它们会尽可能多地匹配，然后回溯。如果在它们后面放置问号（+?、*?、??、{}?），它们会变得懒惰，并开始尽可能少地匹配。懒惰星号会找到能让我们到达 */ 的最小字符片段。它匹配单个块注释。

```
function stripComments(code) {
  return code.replace(/\/\*[\s\S]*?\*\/|\/\/.*?/g, "");
}
console.log(stripComments("1 /* a */+/* b */ 1"));
// → 1 + 1
```

## 动态创建 RegExp 对象

在某些情况下，编写代码时你可能不知道需要匹配的确切模式。如果你想在一段文本中找到用户的名字，并用下划线字符将其包裹以使其突出显示，你可以构建一个字符串并使用 RegExp 构造函数。例如：

```
let name = "harry";
let text = "Harry is a suspicious character.";
let regexp = new RegExp("\\b(" + name + ")\\b", "gi");
console.log(text.replace(regexp, "_$1_"));
// → _Harry_ is a suspicious character.
```

要构建 \b 边界标记，请使用两个反斜杠，因为你是在普通字符串中编写它们。RegExp 构造函数的第二个参数包含正则表达式的选项。"gi" 表示全局且不区分大小写。

```
let name = "dea+hl[|]rd";
let text = "This dea+hl[|]rd guy is super annoying.";
let escaped = name.replace(/[\.\[.+*?{}()|^$]/g, "\\$&");
let regexp = new RegExp("\\b" + escaped + "\\b", "gi");
console.log(text.replace(regexp, "_$&_"));
// → This _dea+hl[|]rd_ guy is super annoying.
```

## search 方法

你不能将正则表达式传递给字符串上的 indexOf 方法。还有另一个方法 search，它确实期望一个正则表达式。与 indexOf 一样，它返回表达式出现的第一个索引，如果未出现则返回 -1。

```
console.log(" word".search(/\S/));
// → 2
console.log("".search(/\S/));
// → -1
```

## lastIndex 属性

exec 方法没有提供一种便捷方式，从字符串中的给定位置开始搜索。正则表达式对象具有属性。其中一个属性叫作 source，它包含创建该表达式的字符串。lastIndex 是另一个属性，在某些有限的情况下，它控制下一次匹配将从哪里开始。正则表达式必须启用全局（g）或粘性（y）选项，并且匹配必须通过 exec 方法发生。例如：

```
let pattern = /y/g;
pattern.lastIndex = 3;
let match = pattern.exec("xyzzyy");
console.log(match.index);
// → 4
console.log(pattern.lastIndex);
```
