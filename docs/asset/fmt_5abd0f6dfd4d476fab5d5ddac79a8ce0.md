
`insertEverywhere x xs =`

  `case xs of`

    `[] -> []`

    `(y:ys) -> x :: y : insertEverywhere x ys`

`permutations : List a -> List a`

`permutations =`

  `foldr (concatMap insertEverywhere) []`

`anagrams : String -> List String`

`anagrams s = toList permutations |> map fromList`

```
该模块说明了函数式编程的一些特征：没有赋值，没有可变变量（我们只有不可变的函数参数），核心库没有控制如何添加新项：函数组合（`<<`）、列表前缀（`::`，由于历史原因读作 cons）以及从右侧折叠（`foldr`）。这些函数的行为如下：
```

```
`(f << g) x -> f(g(x))`

`x :: [a0,...,an] -> [x, a0,...,an]`

`foldr f [a1,a2,a3,a4] -> f(a1,f(a2,f(a3,f(a4,))))`
```

我们现在转向主应用程序，它运行在网络浏览器中。它显示一个文本字段，并对框内容的每次变化做出响应，将所有排列直接渲染在页面上。

## 170 编程语言探索

```elm
import Anagram exposing (anagrams)

import List exposing (map)

import Html exposing (div, text, input)

import Html.Attributes exposing (placeholder, value, maxLength)

import Html.Events exposing (onInput, targetValue)

import Html.App as App
```

```elm
type alias Model = String

type Message = ChangeTo String
```

```elm
main =
  App.beginnerProgram { model = "", view = view, update = update }

update (ChangeTo newModel) model =
  newModel

view model =
  div [
    (input
      placeholder "Text to anagram"
      value model
      maxLength 6
      onInput ChangeTo
    )
  ] : map (\s -> div [text s]) (anagrams)
```

整个程序可能比你预期的要长。部分长度是因为导入了大量的模块，但这表明 Elm 核心库强调了模块化。许多语言都内置了字符串和列表函数，但在 Elm 中，我们需要显式地导入它们。HTML 的 `<div>` 和 `<input>` 元素及其相关的属性和事件在 Elm 中也有表示，我们也必须导入它们。应用程序本身遵循 Elm 架构，这种代码编写风格来自：

- 一个模型（`model`），代表应用程序的“状态”（在这里只是一个字符串），
- 一个视图函数（`view`），它接收当前模型并生成用于渲染的 HTML。HTML 可以包含生成消息的元素。在我们的案例中，有一个 HTML `<input>` 元素可以生成输出事件。我们安排了这些事件发送 `ChangeTo` 消息（`s` 是文本中的字符串），来更新函数。
- 一个更新函数（`update`），它接收消息和当前模型，并生成新模型。在我们的应用中，消息告诉我们具体要做什么：用消息中的字符串更新模型。

我们传统的第三个程序是从标准输入计算单词。为了现在保持简单，我们将硬编码源文本。我们将此项任务留给你，让你练习使用 HTML 文本区域和文件上传来泛化该脚本。

## Elm ■ 171

```elm
import List exposing (map, foldl, repeat)

import Dict exposing (Dict, insert, get, toList)

import String exposing (toLower)

import Regex exposing (regex, find)

import Maybe exposing (withDefault)

import Html exposing (table, tr, td)

import Html.Attributes exposing (style)

message =
  "The fox. It jumped over/under... it did it did the Fox."

countWord : String -> Dict String Int -> Dict String Int

countWord word counts =
  insert word (withDefault 0 (get word counts) + 1) counts
```

```elm
tableCell data =
td [] [toStringData]
```

再次，我们使用了 Elm 的核心模块。脚本本身引入了新的语言特征，但以下内容需要一些解释：

- 提取单词使用了 Elm 的正则表达式匹配，它返回一个包含 Elm 记录（records）的匹配列表。我们将在本章节后面的部分讨论记录。
- 我们将单词及其计数存储在字典（dictionary）中，这是 Elm 在 `Dict` 模块中提供的。字典是持久化数据结构，我们在上一个章节介绍过它们。使用 `get` 字典产生一个 `Maybe`，而 `withDefault` 函数（来自 `Maybe` 模块）作用于 `maybe`。这与 Java、Python、Ruby 以及许多其他语言不同，在那些语言中，字典本身具有感知键的特殊知识。特别是，它们有名为 `getOrDefault` 和 `putAbsent` 的方法。Elm 的字典不需要此类类名：它们在查找时返回 `maybe`。
- Elm 字典要求可比较的键，并且当作为键、值或通过 `toList` 和 `foldl` 函数进行操作时，始终按键的顺序处理。

## 9.2 基础知识

作为一种纯函数式语言，Elm 非常小。事实上，它非常小，以至于我们已经遇到了大部分语法。它具有五种基础类型：`Bool`、`Int`、`Float`、`Char` 和 `String`

172 编程语言探索

- **元组（Tuples）**：值 `("abc")` 的类型是 `(Float, String)`。元组是积类型，它可以包含任意数量的类型。
- **记录（Records）**：值 `{x = 3, y = 5}` 的类型是 `{ String; y = Float }`。记录本质上是带有标签的元组。
- **标签联合（Tagged Unions）**：标签联合（有时称为判别和类型）可以优雅地组合类型，并解决状态机和类型层次结构的问题。稍后我们将看到这种类型类型。
- **函数（Functions）**：值 `{x -> (x,x)}` 的类型是 `Int -> (Int, Int)`。

你期望看到列表？如果你疑惑列表去哪了，别担心——它们是用元组构建的。让我们直接进入示例，第一个示例说明了别名（alias）的使用。别名并没有创建一个新类型，而是为更复杂的表达式提供了一种方便机制。

```elm
import ElmTest exposing (suite, test, runSuite, assertAreEqual)

f : (Int, Int, Int) -> Int

f (a, _, c) =
3 * c + a

type alias Vector = (Float, Float)

magnitude : Vector -> Float

magnitude v =
let (x, y) = v in
sqrt (x * x * y)

main =
runSuite <| "Tuples"
  [ test "语义 =" ((6,8) `assertEqual` (7-1,4*2))
  , test "模式匹配" (f(1,2,3) `assertEqual` 10)
  , test "解构" (magnitude(3,4) `assertEqual` 5.0)
  , test "元组返回" ((x -> (x,x)) `assertEqual` (1,1))]
```

# 174 编程语言探索

| 运算符(s) | 优先级 | 结合性 | 说明 |
|---|---|---|---|
| `<<` | 9 | R | 组合：`(f << g)x = f(g(x))` |
| `>>` | 9 | L | 组合：`(f >> g)x = g(f(x))` |
| `\|` | 8 |  | 幂 |
| `* / //` | 7 |  | 乘法、整除、取模、余数 |
| `% rem` |  |  |  |
| `+` | 6 | L | 加法、减法 |
| `: ++` | 5 | L | 构造、追加 |
| `< <= >=` | 4 | 否 | 小于、小于等于、大于、大于或等于、等于 |
| `= /=` |  |  | 不等于 |
| `&&` | 3 | R | (短路)逻辑与 |
| `\|\|` | 2 | R | (短路)逻辑或 |
| `<\|` | 0 | R | 应用：`f < x = f(x)` |
| `\|>` | 0 | L | 应用：`x > f = f(x)` |

默认情况下，你定义的运算符优先级为 9 且自左结合，但你可以自己设置这些值。在这里我们创建了两个计算 `2x + y` 的运算符，一个高优先级 (8)，一个低优先级 (3)。我们在一个包含乘法（优先级级别 7）的表达式中使用这些运算符，以展示结果。

```
import ElmTest exposing (runSuite, suite, test, assertEqual)

(<-): Int -> Int -> Int

(<-) x y =
2 * x + y

(*<): Int -> Int -> Int

(*<) x y =
2 * x + y

infix 8 <-->
infix 2 **<
main =
runSuite <| "Test own operators with `precedence`"
  [ test "high" < (8 * 3 <-> 5) `assertEqual` 88 -- 8*(2*3+5)
  , test "low" < (8 * 3 << 5) `assertEqual` 53 -- 2*(8+2)+5
  ]
```

我们选择让我们的新运算符具有不可结合性：要设置左结合或右结合，我们将分别使用 `infix` 或 `infixr`。

请注意，标准运算符（加法、乘法、小于等）并没有硬编码到语言中，而是直接在标准库中定义为普通的 Elm 函数。事实上，查看 Elm 编译器的源代码我们可以看到：

```
() : Float -> Float -> Float
() =
Native.Basics.floatDiv
```

infix 7 /

浮点数除法的实现将执行得很快，因为 Elm 编译器可以通过其 `Native.Basics` 模块访问更底层的代码，但点在于，你不会在语言的语法定义中看到运算符；它们仅仅是函数。

关于优先级的最后一点：前缀函数应用的优先级始终高于中缀应用。虽然这非常简单，但这条规则确实会导致一些从其他语言转到 Elm 的程序员可能需要注意的坑：

```
negate 3 ~ parses as (negate 3) ~ 4
show x * y parses as (show x) * y + z
```

当然，正如你预期的，或者像使用优先级为 0 的应用运算符 `<|` 一样：

```
negate <| 3 ~ 4 parses as negate(3 ~ 4)
show <| x * y parses as show(x * y)
```

惊讶的是，这涵盖了大部分基础内容。在本章的剩余部分中，我们将涵盖 ML 家族特色的两个迷点：强大的类型推断机制和标签联合；可扩展记录；以及 Elm 处理交互性的方法（订阅和命令）。

## 9.3 类型推断

Elm 执行类型检查：它在编译时检查表达式的类型，并拒绝执行可能出现类型错误的程序。在执行之前，编译器必须获得关于表达式预期类型的信息，或者足够智能以推断出它们。Elm 的类型推断能力与所有 ML 语言一样，起源在于 Hindley-Milner 类型系统。Java、Swift 和 Rust 在几乎所有变量、方法参数和返回值、类字段上都需要类型注解。让我们从一个非常简单的示例来看 Elm：

```
import String exposing x

mystery (x, y) z =
repeat (
```

标识符没有类型注解，但 Elm 可以推断它们。大致如下：

1. 从左到右工作，我们首先分配类型变量：`x` 得到类型 $\alpha$，因此 `mystery` 得到 $\alpha \to \gamma$。
2. 我们知道 `repeat` 的类型是 `Int -> String`，所以 $\alpha$ 必须是 `Int`。
3. 我们知道 `round` 的类型是 `Float -> Int`，所以 $\gamma$ 必须是 `Float`。
4. 我们知道 `sqrt` 的类型是 `Float -> Float`，所以 `x` 必须是 `Float`。由于我们之前给 `x` 分配了类型 $\alpha$，现在可以将 $\alpha$ 与 `Float` 。
5. `repeat` 的第二个参数必须是字符串，我们将 $\beta$ 与 `String` 。
6. 因为 `repeat` 产生字符串，我们将 $\gamma$ 与 `String` 。
7. 因此，`mystery` 的类型是 `Float -> String`。

让我们看一个更有趣的情况：

```
mystery (x, y) z =
(y / [x, x])
```

在这里我们通过将类型变量 $\alpha$ 映射到 `x`，$\beta$ 映射到 `y`，$\gamma$ 映射到 `z` 开始，从而 $(\alpha, \beta) \to \delta$ 到 `mystery`。我们知道除法 (`/`) 可以推断出 `y` 的类型为 `Float` 并与 `Float` 。我们可以为 `x` 或 `z` 获取任何类型信息，但可以确定函数的类型：`(Float, List \alpha)`。虽然在选择时使用希腊字母作为类型变量是种习惯，但 Elm 对类型变量使用小写字母，并报告 `mystery` 的类型为 `(a, Float) -> b -> (Float, List a)`。通常，类型变量与任何类型统一，但 Elm 有仅与特定类型统一的特殊类型变量：

- `unify`：仅与 `Int` 和 `Float` 统一，支持函数 `(+)`、`(-)` 和 `(*)`；
- `comparable`：仅与 `Int`、Char、String、包含 comparable 的元组类型以及包含 comparable 的列表类型统一，支持 `<`、`<=`、`>`、`>=`、min、max；
- `appendable`：仅与 `String` 和列表类型统一，支持 `++`。

Elm 中这些特殊类型的示例包括：

```
-- From Basics
(>) : comparable -> Bool
abs : number -> number
(++) : appendable -> appendable
```

> 在这种情况下，统一似乎是将类型变量实例化为具体类型；然而，在更复杂的情况下，我们可能会发现两个类型变量指向同一种类型，并需要“统一”为一种类型。

> 然而奇怪的是，在检查既是 comparable 又是 appendable 的表达式时，会出现第四种变量 `compound`。你可能会看到它“泄漏”到你的世界中，当编译器告诉你 `x y = if (x < y) then (x ++ y) else (y ++ x)` 的类型为 `compound -> compound -> compound`；然而，编译器不会尊重你对该变量的使用。你将在练习中进行进一步探索。

```
-- From List
sum : List number -> number
maximum : List number -> Maybe comparable
sort : List comparable -> List comparable
sortBy (a -> comparable) -> List -> List a
```

```
-- From Set（注意特殊元素必须是 comparable）
insert : comparable -> Set comparable -> Set comparable
member : comparable -> Set comparable -> Bool
```

```
-- From Dict（注意字典键必须是 comparable）
insert : comparable -> v -> Dict v
member : comparable -> Dict v -> Bool
get : comparable -> Dict v -> Maybe v
```
