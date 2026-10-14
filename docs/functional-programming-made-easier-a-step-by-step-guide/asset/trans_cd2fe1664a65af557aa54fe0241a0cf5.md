

我们可以看到下面的函数如何让我们为每种类型获取 Directions：

```
getPersonDirections :: Person -> Directions
getPersonDirections (Person person) = getDirections person.address ①

getCompanyDirections :: Company -> Directions
getCompanyDirections (Company company) = getDirections company.address ①

getResidenceDirections :: Residence -> Directions
getResidenceDirections residence = getDirections $ case residence of ②
  Home address -> address
  Facility address -> address
```

① record.fieldName 是我们访问记录字段的方式。

② 我们必须为 Residence 使用 case 表达式，因为它是一个 Sum Type。

顺便说一下，我们可以用几种不同的方式编写 getResidenceDirections：

```
getResidenceDirections' :: Residence -> Directions
getResidenceDirections' = getDirections <<< case _ of ①
  Home address -> address
  Facility address -> address

getResidenceDirections'' :: Residence -> Directions
getResidenceDirections'' = getDirections <<< go where ②
  go (Home address) = address
  go (Facility address) = address
```

① 点自由写法，其中 case 表达式使用通配符变量，即 Residence 值。

② 使用局部函数 go 的点自由写法，该函数使用 Pattern Matching 而不是 case 表达式。

编写这些函数相当简单，但当你尝试在同一个函数中使用它们时会发生什么？

让我们尝试编写一个函数来接收这三种类型：

```
getDirectionsTo :: ??? -> Directions
```

问题是我们希望 getDirectionsTo 接受 Person、Company 或 Residence。但那是什么类型？

注意我们使用了“OR”这个词。这应该提示我们如何统一这些类型。我们需要创建一个 Sum Type：

```
data HasAddress
  = PersonAddress Person
  | CompanyAddress Company ①
  | ResidenceAddress Residence ①
```

① 注意使用 OR 符号，|。这表示 HasAddress 等于 PersonAddress 或 CompanyAddress 或 ResidenceAddress。

现在我们有一个单一的类型，可以涵盖所有具有 Address 的类型以传递给 getDirectionsTo：

```
getDirectionsTo :: HasAddress -> Directions
getDirectionsTo = case _ of
  PersonAddress (Person person) -> getPersonDirections person
  CompanyAddress (Company company) -> getCompanyDirections company
  ResidenceAddress residence -> getResidenceDirections residence
```

起初我们可能对解决方案感到满意，但当我们的代码库中出现新的具有 Address 的类型时会发生什么？

```
data EmptyLot = EmptyLot
  { daysEmpty :: Int
  , price :: Int
  , address :: Address
  }
```

现在我们必须编写以下内容：

```
getEmptyLotDirections :: EmptyLot -> Directions
getEmptyLotDirections lot = getDirections lot.address
```

不算太糟糕，但我们还没做完。getDirectionsTo 需要更新，Sum Type HasAddress 也需要更新：

```
```haskell
data HasAddress
  = PersonAddress Person
  | CompanyAddress Company
  | ResidenceAddress Residence
  | EmptyLotAddress EmptyLot

getDirectionsTo :: HasAddress -> Directions
getDirectionsTo = case _ of
  PersonAddress (Person person) -> getPersonDirections person
  CompanyAddress (Company company) -> getCompanyDirections company
  ResidenceAddress residence -> getResidenceDirections residence
  EmptyLotAddress lot -> getEmptyLotDirections lot
```
```

+   1. 将我们的新类型添加到 Sum Type 中。
+   2. 添加 `EmptyLot` 的 case。

这可能看起来不算太糟，但想象一下我们现在想要编写一个函数来计算到地址的距离。现在我们需要另一个像 `getDirectionsTo` 这样的函数来计算距离：

```
```haskell
newtype Miles = Miles Int

getMilesTo :: HasAddress -> Miles
getMilesTo = case _ of
  PersonAddress (Person person) -> getPersonMiles person
  CompanyAddress (Company company) -> getCompanyMiles company
  ResidenceAddress residence -> getResidenceMiles residence
  EmptyLotAddress lot -> getEmptyLotMiles lot
```
```

+   1. 我们创建一个 `newtype` 来包装 `Int`，表示英里数而不是公里数。
+   2. 需要编写 `getPersonMiles`。
+   3. 需要编写 `getCompanyMiles`。
+   4. 需要编写 `getResidenceMiles`。
+   5. 需要编写 `getEmptyLotMiles`。

所以现在我们有一整套其他函数需要编写。不太好。

让我们通过编写一个单一的 `getMiles` 函数并使用它来修复这个问题：

```
getMiles :: Address -> Miles
getMiles address = ... ①

getMilesTo :: HasAddress -> Miles
getMilesTo = getMiles $ case _ of ②
  PersonAddress (Person { address }) -> address ③
  CompanyAddress (Company { address }) -> address ④
  ResidenceAddress (Home address) -> address ⑤
  ResidenceAddress (Facility address) -> address ⑥
  EmptyLotAddress (EmptyLot { address }) -> address ⑦
```

① 细节在这里不重要。

② 在这里我们用 case 表达式的值，即一个 Address，来调用 getMiles。

③ 我们模式匹配 Person 并解构其 Record 以获取 address 字段。

④ 我们模式匹配 Company 并解构其 Record 以获取 address 字段。

⑤ 我们模式匹配 Home。

⑥ 我们模式匹配 Facility。注意我们在这里再次提及 ResidenceAddress，唯一的区别是我们匹配的是哪个 Residence 构造子。

⑦ 我们模式匹配 EmptyLot 并解构其 Record 以获取 address 字段。

采用这种方法我们不需要编写那么多函数，但维护 Sum Type 并更新 case 表达式仍然很麻烦，不仅在这个函数中，而且在接受我们 Sum Type 的每一个函数中。

## 6.2. 解决方案

我们到目前为止所做的一切都是样板代码。当你不需要太多思考就可以复制粘贴现有解决方案并做少量修改来获得新函数或 case 时，你就知道它是样板代码。

复制粘贴应该是提醒你更通用的解决方案是可取的并且希望是可能的红旗。有时技术限制会迫使你创建样板代码。但在我们的例子中，我们只需要一种方法来指定 Person、Company、Residence 和 EmptyLot 都有地址。

如果它们都是记录的类型别名，那么我们就可以简单地使用 ._address 作为我们的访问函数（使用通配符表示 Record）。但其中一个是 Sum Type，即 Residence，所以这对我们不起作用。

当我们想在 C# 或 Java 等语言中以类似的方式处理不同的事物时，我们使用接口：

```
```java
// Java
public interface HasAddress {
    Address getAddress();
}
```
```

```
```csharp
// C#
interface IHasAddress
{
    Address getAddress();
}
```
```

在这些语言中，对象只需要支持接口，然后在代码中任何想要处理 JUST `Addresses` 的地方，都可以将接口传递给你的函数。

但在 PureScript 和 Haskell 中，我们没有对象。取而代之的是，我们有类型。

幸运的是，我们可以通过创建 *Typeclasses* 来对类型进行分组，并使我们的类型成为该 Typeclass 的 *Instance*。

为了更好地理解这一点，让我们先创建 Typeclass `HasAddress`：

```
```haskell
class HasAddress a where
    getAddress :: a -> Address
```
```

+   1. 我们使用 `class` 关键字创建 Typeclass。
+   2. 注意这个类有一个单一的类型参数 `a`。在定义实例时我们会把我们的类型放在这里。
+   3. 这里列出创建 Typeclass 实例必须实现的所有函数。在这种情况下，我们只有一个。

类型参数 `a` 代表实现类实例的类型。所以让我们为 `Person` 编写实例：

```
```haskell
instance hasAddressPerson :: HasAddress Person where
    getAddress (Person p) = p.address
```
```

将期望 Person 作为其第一个参数。

③ 我们解构 Person 以获取底层 Record，然后访问 address 字段。

花点时间想象如何为 Company、Residence 和 EmptyLot 编写实例。这些将镜像上面的 hasAddressPerson，除了 Residence 因为它是 Sum Type。

以下是这些实例：

```
instance hasAddressCompany :: HasAddress Company where
    getAddress (Company c) = c.address

instance hasAddressResidence :: HasAddress Residence where ①
    getAddress (Home address) = address
    getAddress (Facility address) = address

instance hasAddressEmptyLot :: HasAddress EmptyLot where
    getAddress (EmptyLot l) = l.address
```

① Residence 的实例使用 Pattern Matching 有多个版本的 getAddress。

有了这个新特性，让我们重写 getDirections：

```
-- WILL NOT COMPILE!!!
getDirections :: ∀ a. a -> Directions ①
getDirections hasAddr = let address = getAddress hasAddr in ②
    ... ③
```

① 签名错误。

② 通过调用 getAddress，我们期望 hasAddr 具有 HasAddress 实例。

③ 细节在这里不重要。

但这不能编译。为什么呢？

## 6.3. 约束

我们告诉编译器 a 可以是任意类型，但我们却像它有 HasAddress 实例一样使用 a。我们需要一种方法让编译器知道 a 可以是任意类型，但它也必须具有 HasAddress 实例。

我们使用约束来实现这一点：

