

## 第七部分：附录

## JavaScript 速查表

### JavaScript 速查表口袋指南

并非有意穷尽所有内容，但包含了最精华的部分和大量实用建议与技巧。v1.0。

## 内置类型与字面量

| 类型 | 字面量示例 |
| 数字 | `0`, `42`, `0.15`, `3e10`, `-3.12e-2` |
| 字符串 | `"Hello"`, `'hello'`（两者都允许转义）。常见转义：`\r`, `\n`, `\t`, `\\`, `\"`, `\'`, `\uXXXX`（十六进制）, `\0ooo`（八进制） |
| 布尔值 | `true`, `false` |
| 数组 | `[]`, `[1, 2, 3]`, `[[[]], 2, 1]`... |
| 日期 | `new Date(...)`（没有字面量表示法）|
| 正则表达式 | `/pattern/flags`（参见专门的一页）|
| 函数 | `function(...) {...}`（参见专门的一页）|
| 对象 | `{ prop: value, prop2: value2... }` |

`typeof` 表达式 -> 类型名称，小写。

布尔转换：`0`、`''`（空字符串）、`null` 和 `undefined` 被视为假。其他一切值都被视为真。

## 正则表达式要点

| 正则表达式特性 | 语法 |
| 字符类（匹配字符集） | `\d` `\D` `\w` `\W` `\s` `\S` `[...]` `[^...]`（字面连字符必须放在末尾）|
| 边界 | `\A` `\Z` `^` `$` `\b` `\B` |
| 贪婪量词（最大匹配） | `*`（0+）, `?`（0-1）, `+`（1+）, `{min,}`, `{max}`, `{min,max}` |
| 惰性量词（最小匹配） | `*?`, `??`, `+?` |
| 分组 | `(...)` 捕获（可反向引用），`(?:...)` 不捕获（更快）|
| 前瞻 | `(?=...)` 要求匹配，`(?!...)` 要求不匹配 |
| 反向引用 | `\1`...`\9`（捕获组），`\&`（整个匹配）|
| 分支 | \| （如果在组内，则仅限于该组）|

### 标志

| 标志 | 含义 |
| `g` | 全局匹配：不仅匹配第一个匹配项，而是匹配所有匹配项。 |
| `i` | 不区分大小写（也支持 Unicode！）|
| `m` | 多行：点号字符 `.` 匹配任何字符，包括换行符 |

- 反复编译正则表达式速度很慢：请预编译成常量。
- 如果只需要测试是否存在匹配，而不关心细节（分组等），请使用 `regex.test(str)` 而不是 `str.match(regex)`。
- 如果不需要捕获分组供以后引用，而只是需要对分组应用量词，请将分组标记为不捕获：`(?:...)`。

## 函数

- 声明：`function fName(...) { ... }`
- 表达式：`function(...) { ... }`

声明会在其作用域内被“提升”：无论顺序如何，任何声明都可以使用其他任意一个声明（不需要“原型声明”）。

- `"return x;"` 使用返回值 x 退出函数。
- `"return;"` 使用返回值 `undefined` 退出函数。

函数与其他对象一样，也有自己的方法（例如 `apply`、`call`），并且可以通过引用传递（但会丢失它们的绑定：它们对 `this` 关键字的原始含义）。这意味着你可以将它们赋值给变量，并作为参数传递，等等。

参数列表不指定类型，只是作为“提示”，自动将名称分配给实际传递的前几个参数。但任何 JS 函数都是“可变参数”的：你可以传递任意多的参数，并通过内置的 `arguments` 变量访问它们，该变量行为很像数组（它具有 `length` 和 `[]`）。

## 特殊值

| 值 | 描述 |
| `undefined` | 尚未有值的变量，参数没有匹配的传入实参。 |
| `null` | 不完全是 undefined；通常是“无结果”DOM 调用的值，也是一种以编程方式为某事物赋予“无值”的方法。 |
| `false`, `true` | 两个布尔字面量。 |
| `Infinity` | 数值无穷大（可以有符号，例如 `-Infinity`）。|
| `NaN` | 非数值（Not-a-Number）表达式的结果，例如数字解析失败。它不等于任何数值，包括它自身。请使用 `isNaN(n)` 进行正确检测。 |

## 运算符

### 算术：`+ - * / % ++ --`

记住：没有整数/浮点之分，只有数字！

`%` = 取模/余数。一元减号反转符号：`-42`。`++` 和 `--` 递增/递减。除非有明确的理由使用后缀形式（`x++`），否则请优先使用前缀形式（`++x`）。

### 比较：`== === < <= > >= !==`

`==` 只比较值，使用“转换协议”。因此 `5 == "5"`。`0 == false`，`null == undefined`。`===` 进行严格比较：值 + 类型。非常适合测试 `undefined === x`。`!=` 表示不相等（类似于 VB/SQL 的 `<>`）。

### 布尔逻辑：`&&`（与）`||`（或）

只需记住：

- `&&` 优先于 `||`
- `a || b` 如果 `a`（...转换为真），则短路（不计算）`b`
- `a && b` 除非 `a` 为真，否则短路（不计算）`b`

### 算术简写：`+= -= *= /= %=`

`a += b` 的行为类似于 `a = a + b`，以此类推。更简洁！

### 成员选择：`[..]`

- 按索引选择数组：`array[5]`（从 0 开始）。
- 动态成员选择：
  - `obj["propName"]` <=> `obj.propName`
  - `obj["methodName"](...)` <=> `obj.methodName(...)`
  - 例如：`node[visible ? 'show' : 'hide']();`

### 优先级：与 C++/Java/Ruby 的大致相同...

- `* / %` 优先于 `+`
- `&&` 优先于 `||`
- `(...)` 强制优先级
- `(5 * 3) + (6 / 2)` <=> `5 * 3 + 6 / 2`
- `(a & b) || (c & d)` <=> `a & b || c & d`

### 位运算（很少需要）：`& | ^ << >> >>>`

`^` 是异或，`<<` 和 `>>` 移动位（`>>>` 带符号丢失 / 零填充）。

## 变量与作用域

```js
var x, y = 42, z, t = y * z;
```

局部变量必须使用 `var` 声明。你应该尽量避免使用或泄漏全局变量。

变量可以在声明时即时赋值。它们可以在其所在作用域（通常指当前函数）中的任何位置访问。

如果你的代码需要隐藏某些标识符（无论是变量还是函数），请使用模块模式：

```js
(function() {
  // what's in here stays in here unless you explicitly
  // bring it out by return or direct assignment.
})();
```

## 决定走哪条路径

```js
if (condition) {
  code
}

if (condA) {
  codeA
} else if (condB) {
  codeB
} else {
  codeC
}
```

```js
switch (expr) {
  case valueA:
    codeA
    break;
  case valB1:
  case valB2:
    codeB
    break;
  default:
    codeC
}
```

高手提示：尽早使用带返回值的测试，可以避免将其余代码嵌套在 `else` 块中，并保持缩进整洁！

## 循环

```js
for (decl; test; incr) {
  code
}

do {
  codeRunAtLeastOnce
} while (cond)
```

```js
while (cond) {
  codePerhapsNeverRun
}

while (true) {
  codeRunAtLeastOnce
  if (!skipRestOfTurn)
    continue;
  if (justStopLooping)
    break;
  remainderCode
}
```

“快速数组循环”：

```js
for (var i = 0, l = arr.length; i < l; ++i)
  code
```

## 你应该了解的数组操作

```js
var arr = [2, 3, 4, 5, 6];

arr = arr.concat([7, 8, 9])  // => [2, 3, 4, 5, 6, 7, 8, 9]
arr                          // => [2, 3, 4, 5, 6, 7, 8, 9]
arr.push(10)                 // => [2, 3, 4, 5, 6, 7, 8, 9, 10]
arr.unshift(1)               // => [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
arr.pop()                    // => 10
arr.shift()                  // => 1
arr.slice(4, -1)             // => [6, 7, 8]
arr.join('')                 // => '23456789'

arr.sort(function(a, b) {
  return b - a;
})                            // => [9, 8, 7, 6, 5, 4, 3, 2]
arr.sort()                    // => [2, 3, 4, 5, 6, 7, 8, 9]
arr.splice(5)                 // => [7, 8, 9]
arr                           // => [2, 3, 4, 5, 6]
```

## 真正实用的字符串操作

```js
'yay'.charAt(1)                // => 'a'
'hello'.indexOf('l')            // => 2
'hello'.indexOf('l', 3)         // => 3 (specified min pos)
'hello'.lastIndexOf('l')        // => 3
'hello'.lastIndexOf('l', 2)     // => 2 (specified max pos)
'hello'.replace(/l/, 'L')       // => 'heLlo'
'hello'.replace(/[aeiou]/g, '-') // => 'h-ll-'

'hello'.replace(/[a-z]/g, function(s) {
  return s.toUpperCase();
}) // => 'HELLO'

'a b c'.split(' ')              // => ['a','b','c']
'a b c'.split(/\s+/)           // => ['a','b','c']
'abc'.split('')                 // => ['a','b','c']
'a b c'.split(' ', 2)           // => ['a','b'] (specific max count)
'hello'.substring(2)            // => 'llo'
'hello'.substring(2, 4)         // => 'll' (specified end boundary)
'hello'.slice(-3)               // => 'llo' (start 3 from end)
'hello'.slice(3, -1)            // => 'l' (specified end boundary, 1 from end)
'Elodie'.toLowerCase()          // => 'elodie'
'déjà ça'.toUpperCase()         // => 'DÉJÀ ÇA'
'hello'.match(/(l)/)            // => ['l','l']
// full match at index 0, captured group 1 at index 1, etc.
```

## 异常/错误处理

```js
try {
  thisCodeMayExplode
} catch(e) {
  thisCodeRunsOnlyOnErrors // e refers to the error object
} finally {
  thisCodeRunsWhetherOrNotThereIsAnError
}
```

你可以使用 `throw exceptionObject` 抛出自己的错误（任何对象都可以）。

## 数学函数

## 一些全局实用功能

## 异步代码：使用超时

## 穷人的调试器

## 标识符和保留字

