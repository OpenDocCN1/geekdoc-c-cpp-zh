
```
getDirections :: ∀ a. HasAddress a => a -> Directions
getDirections hasAddr = let address = getAddress hasAddr in
  ...
```

❶ 类型 a 必须是 HasAddress 的一个实例。

❷ 这里的细节不重要。

HasAddress a => 是将 a 约束为具有 HasAddress 实例的类型的语法。

你可以在一个类型签名中包含多个约束：

```
getDirections :: ∀ a. Show a => HasAddress a => a -> Directions
getDirections hasAddr = let address = getAddress hasAddr in
  ...
```

❶ 类型 a 必须同时是 Show 和 HasAddress 的实例。

❷ Show 是一个用于可以表示为字符串的类型的类型类。

❸ 这里的细节不重要。

注意约束是如何位于 ∀ a. 和类型参数之间的。

你也可以使用圆括号将类型类用逗号分隔来定义多个约束：

```
getDirections :: ∀ a. (Show a, HasAddress a) => a -> Directions
```

当我的签名都在一行时，我倾向于使用圆括号版本；当我的类型签名跨多行时，则恢复为更冗长的签名：

```
getDirections
  :: ∀ a
  . Show a
  => HasAddress a
  => a
  -> Directions
```

现在我们有了类型类，只需为 Person 编写以下代码：

```
class HasAddress a where
    getAddress :: a -> Address

data Person = Person
    { name :: String
    , age :: Int
    , address :: Address
    }

instance hasAddressPerson :: HasAddress Person where
    getAddress (Person p) = p.address

getDirections :: ∀ a. HasAddress a => a -> Directions
getDirections hasAddr = let address = getAddress hasAddr in
    ... ①
```

① 这里的细节不重要。

如果我们要添加 Company，只需实现以下代码：

```
data Company = Company
    { name :: String
    , address :: Address
    }

instance hasAddressCompany :: HasAddress Company where
    getAddress (Company c) = c.address
```

现在我们可以将 getDirections 用于 Company，而无需更改 getDirections。

借助类型类，我们可以轻松地以类似方式处理不同的类型，而无需创建和类型（Sum Type）。也不需要 case 表达式。编译器在编译时确定我们引用的是哪个类型。

这大大降低了复杂性和样板代码。

## 6.4. 类型类要求

每个类型类函数都称为一个方法：

```
instance hasAddressPerson :: HasAddress Person where
    getAddress (Person p) = p.address ①
```

① getAddress 是类型类 HasAddress 唯一的方法。

请不要将此与面向对象的方法混淆。虽然使用了“类”和“方法”这两个词，但在这里含义不同。

类型类有一个起初可能并不明显的要求。

每个类型类方法必须在其类型签名中包含其多态参数。

原因在于，调用 getAddress 不足以确定要调用哪个 getAddress，因为许多类型都可以是 HasAddress 的实例。编译器需要有一个类型来确定调用哪个 getAddress。

如果我们回顾一下我们的类，可以看到每个方法（一共 1 个）都需要 a 作为其参数之一：

```
class HasAddress a where
  getAddress :: a -> Address ①
```

① 要求将 a 作为第一个参数。该信息足以让编译器确定要使用哪个 HasAddress 实例。

暂且让我们想象一下没有这个限制的情况：

```
-- COMPILER ERROR!!
class HasAddress a where
  getAddress :: Address
```

以下是具体的错误：

![](img/8c0e9b687c62642e828ccb5481e11313_246_0.png)

错误指出有一些“参数”无法确定，即 a。

## 6.5. 内置类型类

在 PureScript 中有许多内置类型类。我们即将查看的大多数类型类在 Haskell 中都有等价（如果不完全相同）的版本。

### 6.5.1. Eq 类型类

该类型类用于比较同一类型的两个值是否相等。

以下是定义：

```
class Eq a where ①
  eq :: a -> a -> Boolean ②

infix 4 eq as == ③
```

① 该类有一个类型参数 a。

② 注意 eq 的类型签名中包含了类型参数 a。

③ 运算符 (==) 是 eq 函数的中缀版本。它没有结合性，这意味着当在一个表达式中使用多个此类运算符时，我们必须添加括号。

让我们为 Person 编写一个实例：

```
data Person = Person
  { name :: String
  , age :: Int
  , address :: Address
  }

instance eqPerson :: Eq Person where
  eq (Person p1) (Person p2) = ??? ①
```

① 我们已经解构了两个 Person 值以暴露其底层的记录。

现在我们卡住了。我们需要确定什么意味着两个 Person 相同。根据你的类型的语义（基于你所建模的内容），我们在这里可能会有完全不同的实现。

在这种情况下，我们假设如果记录的所有字段都相等，则 Person 值相等：

```
instance eqPerson :: Eq Person where
  eq (Person p1) (Person p2) =
    p1.name == p2.name && p1.age == p2.age && p1.address == p2.address ①
```

① String（name）、Int（age）和记录（Address）都有 Eq 的实例。

我们很幸运。我们不必让任何字段类型成为 Eq 的实例，因为它们已经是了。

然而，如果 Address 被定义为一个真正的类型，而不仅仅是一个类型别名：

```
data Address = Address
  { street1 :: String
  , street2 :: String
  , city :: String
  , state :: String
  , zip :: String
  }
```

我们的 Eq 实例会出现以下错误：

![](img/8c0e9b687c62642e828ccb5481e11313_248_0.png)

现在编译器在寻找 Eq Address 的类型类实例。之前，Address 只是记录的别名，而记录有 Eq 实例。

但现在 Address 是它自己的类型，我们需要添加一个 Eq 实例：

```
instance eqAddress :: Eq Address where
  eq (Address a1) (Address a2) = a1 == a2 ① ②
```

① 解构两个 Address 值以暴露其底层的记录。

② 在使用 == 时，我们利用了记录的 Eq 实例。

记录只有在所有字段类型也都具有 Eq 实例时才能进行相等性比较。在我们的例子中，Address 中的每个字段都是 String 类型，而 String 有 Eq 实例。

以下是我们最终的实现：

```
data Address = Address
  { street1 :: String
  , street2 :: String
  , city :: String
  , state :: String
  , zip :: String
  }

data Person = Person
  { name :: String
  , age :: Int
  , address :: Address
  }

instance eqPerson :: Eq Person where
  eq (Person p1) (Person p2) =
    p1.name == p2.name && p1.age == p2.age && p1.address == p2.address

instance eqAddress :: Eq Address where
  eq (Address a1) (Address a2) = a1 == a2
```

### 6.5.2. Ord 类型类

该类型类用于确定同一类型的两个值的顺序。

以下是定义：

```
class Eq a <= Ord a where ①
  compare :: a -> a -> Ordering

data Ordering = LT | GT | EQ ②
```

① 反向胖箭头是一个超类约束。

② 这个和类型定义了同一类型任意两个值之间 3 种可能的排序。

可以说 Eq 是 Ord 的超类。这并不像继承。它仅仅意味着任何 Ord 实例也必须是 Eq 实例。

如果我们在 Pursuit 中查阅 Ord，我们会看到以下内容：

## Ord

```
class (Eq a) <= Ord a where
```

`Ord` 类型类表示支持全序比较的类型。

`Ord` 实例应满足全序的定律：

+   - 自反性：`a <= a`
+   - 反对称性：如果 `a <= b` 且 `b <= a`，则 `a = b`
+   - 传递性：如果 `a <= b` 且 `b <= c`，则 `a <= c`

# 成员

+   - `compare :: a -> a -> Ordering`

# 实例

+   - `Ord Boolean`
+   - `Ord Int`
+   - `Ord Number`
+   - `Ord String`
+   - `Ord Char`
+   - `Ord Unit`
+   - `Ord Void`
+   - `(Ord a) => Ord (Array a)`
+   - `Ord Ordering`
+   - `(RowToList row list, OrdRecord list row) => Ord (Record row)`

注意大多数原始类型都有 `Ord` 实例，例如 `Boolean`、`Int`、`String` 等。但也有一些奇怪的，例如 `Unit`、`Void` 和 `Ordering`。

`Unit` 的实例会是什么样子？

试着在不继续阅读的情况下编写它。

为 `Unit` 编写实例通常非常简单：

```
instance ordUnit :: Ord Unit where
  compare _ _ = EQ ① ②
```

① 这里我们使用惯用的实例命名方式。先是类名 `ord`，然后是类型名 `Unit`，得到 `ordUnit`。

② `Unit` 只有一个成员，即 `unit`。一切事物都等于自身（数学中的自反性）。

