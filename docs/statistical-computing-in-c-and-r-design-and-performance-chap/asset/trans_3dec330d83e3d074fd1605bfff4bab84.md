

## 创建新类

一个 "regr" 类的对象
槽 "X":
<0 x 0 matrix>

槽 "y":
numeric(0)

槽 "b":
numeric(0)

槽 "intercept":
logical(0)

这表明已经构建了一个“空白”的 regr 对象，其类成员/槽（slots）已分配了与其类对应的 R 默认对象。

在某些情况下，为给定类提供的新默认值（或它们传播到从用户定义类构建的类中的方式）可能并不理想。在 C++ 中，这种对构造函数中默认参数的解决方法在 R 中同样适用。但 R 提供了另一种方法，在通过 `setClass` 函数首次创建类时，使用 `prototype` 函数来实现。例如，在我们的 regr 中，X 矩阵可以指定默认值为包含单个元素的 1 x 1 "matrix"，y 和 b 槽可以设为 0，而 intercept 可以设为 1, 1。后者将使常数项成为默认拟合行为。这可以通过以下方式实现：

```R
setClass("regr", representation(X = "matrix", y = "numeric",
b = "numeric", intercept = "logical",
prototype(X = matrix(0, 1), y = 0, b = 0, intercept = TRUE))

> regrObj <- new("regr")
> regrObj
An object of class "regr"
Slot "X":
[1] 0
Slot "y":
[1] 0
Slot "b":
[1] 0
Slot "intercept":
[1] TRUE
```

输出显示使用 `new` 算符创建的 regrObj 为 X、b 和 intercept 槽产生了指定的默认条目。让我们使用特定数据集创建一个 regr 对象。为了这个目的，我们将使用 `mtcars` 数据框的一部分，它包含了 1974 年《Motor Trend》杂志报道的 32 辆汽车的测量数据和其他特征。该数据集通过 `data(mtcars)` 加载到 R 环境中。我们 regr 对象的槽将由 mtcars 数据框的第一列填充（对应每加加仑油量），而 X 槽将由第 3、6 和 7 列组成，分别给出排量（立方英寸）、重量和四分之一英里速度。为了完成“在 R 中创建类和方法”，首先创建此包含用于 regr 对象的信息的矩阵：

```R
A <- as.matrix(c(1, 3, 6, 7))
```

可以通过以下方式获取所需的 regr 对象：

```R
> regrCar <- new("regr", X = A[2:4], y = A[1])
```

可以使用 `@` 算符或 `slot` 函数访问对象的槽。因此，如果 Obj 是一个名为 Obj 的对象，那么 `Obj@` 或 `slot(obj, "b")` 将返回该特定槽的内容。下面的代码列出了如何使用 `@` 和 `slot` 来填充用 mtcars 数据创建的 regr 对象的 b 槽：

```R
> XTX <- t(cbind(1, regrCar@X))**% reggrCar@y
> regrCb <- solve(XTX, drop(cbind(1, regrCar@X)))
> regrCb@b
```

| disp | wt | qsec |
| :--- | :--- | :--- |
| 19.7755755 | -5.034409167 | 0.926492353 |
| slot(regrCar, "b")[1] | 19.7756 | |

进入 b 槽的值是 y 对 X 回归中系数的最小二乘法估计值。访问 regrCar 的 X 槽，由于 intercept 为 TRUE，因此向矩阵中添加了元素个数，使得回归包含一个截距项。结果 X 矩阵被评估，并存储为 XTX，然后使用 `solve` 计算。该函数将在下一节中详细讨论。现在只需要知道，只要 A 是奇异矩阵，调用 `solve(A, v)` 将返回系统 $Ab = v$ 的 $b$。在特定实例中，`solve` 应用于 $A = matrix, v = t(cbind(1, regrCar@X)) \*% reggrCar$，得到的解被赋值给 regr 的 b 槽。这里有一个有趣的点，是在 `solve` 处理的线性系统右侧对 `cbind(1, regrCar)` 使用了 `drop`。这里的问题是，`regrCar@y` 与矩阵对象 `cbind(1, regrCar@X)` 的乘法将对象提升为矩阵状态，并赋值给了 b 槽。一种方法是简单的使用 `drop` 函数将结果强制转换为右，它会删除只有一个列或一行的数组中的多余维度。直接使用 `new` 算符构建特定类的每个对象可以根据实践中的特定情况进行定制。与 C++ 一样，构造函数的名称通常与其类名相同，并涉及在特定情况下创建对象所需的参数。构造函数的创建方式与 R 中的相同。一个 regr 类的构造函数可能如下：

```R
regr <- function(X, y, intercept = TRUE) {
  regrCb <- new("regr", X = as.matrix(X), y = as.numeric(y))
  intercept <- intercept
  if(intercept){
    XTX <- t(cbind(1, regrCb@X))**%reggrCb@X
    regrCb@b <- solve(XTX, drop(cbind(1, regrCb@X)))*%regrCb@y)
  }
```

## 创建新类

```R
else{
  XTX <- t(regrObj@X)**%regrObj@X
  regrObj@b <- solve(XTX, drop(regrObj@X)*regrObj@y)
}
```

注意构造函数中内置了保护机制，尝试将 X 和 y 转换为适当的类。这在意外提供 X 参数时起到了作用。此外，通过在参数列表中指定默认值，强制了包含截距项的行为。使用 mtcars 数据使用 regr 类构造函数现在产生如下结果：

```R
> regrCar <- regr(A[2:4], A[1])
> regrCar
```

| wt | qsec |
| :--- | :--- |
| 19.7755755 | -5.034409167 | 0.926492353 |
| regrCar <- regr(A[2:4], A[1], FALSE) | |

```R
> regrCar
0.0151905 -5.9904330 2.00209915
```

带有和不带截距项的结果已获得。为了确定哪个更好，可以扩展 regr 类以包含拟合的衡量（练习 6.2）。通常检查对象是否以正确方式构建是良好的做法。这会自动处理像 matrix 等指定的类。当调用 `new` 时 X 槽必须提供矩阵，否则将发生错误。但没有进一步的检查来确保任何一致性或构造函数内部的计算是可能的。

对于 regr 类型的对象，预期一个特征是 X 和 y 数组具有相同的行数。类的 `nrow` 函数允许我们进行此类比较。此外，为了工作，矩阵 X（或由单位向量扩展的 X）必须满秩。可以使用 R 函数 `qr` 来检查此条件。该函数返回一个带有指定矩阵秩的列表。我们将在 7.5 节中使用 `qr` 函数。

为了确保用户创建类的输入数据是合适的，可以使用 `setValidity` 函数。下面的代码采用此函数来检查 X 和 y 槽的长度以及适当的

```R
setValidity("regr", object){
  if(nrow(object@X) != length(object)){
    return("The number of rows for X and y differ")
  }
  if(object@intercept){
    if(qr(cbind(1, object@X))$rank < ncol(object@X)+1){
      return("The matrix is singular")
    }
  } else{
    if(qr(object@X)$rank < ncol(object@X)){
      return("The matrix is singular")
    }
  }
  return(TRUE)
}
```

## 在 R 中创建类和方法

面向语言的多态特性之一是拥有扩展基类的继承类。R 中的继承机制非常简单，除非 `setClass` 函数指定了额外的 `contains` 参数。对于我们的目的，`contains` 将是一个给出父类名的字符串。为了在 R 中说明，假设感兴趣通过包含一个对应值的额外成员来扩展 regr 类。再次，已经有此类工具将其作为原始 regr 类的槽。为了说明目的，我们将忽略这些问题，并像有理由区分拟合或不拟数据的 regr 对象类型一样进行。

让我们考虑我们的新类 `regrFit`。该类的创建类似于 regr 类，使用：

```R
setClass("regrFit", contains="regr", representation = list(yhat = "numeric", prototype(yhat = 0)))
```

这与我们创建 regr 类不同，在于 `setClass` 中存在 `contains` 参数，其设置为 `regr`，表示 `regrFit` 是 regr 的派生类。regrFit 类的对象将自动继承 regr 类的所有槽：即 X、y 和 intercept。只需要定义命名为 yhat 的值的新槽即可。

下一步是创建一个类构造函数：

```R
regrFit <- function(X, y, intercept = TRUE){
  fitObj <- regr(X, y, intercept)
  fitObj <- as(fitObj, "regrFit")
  if(fitObj@intercept)
    fitObj@yhat <- drop(cbind(1, fitObj@X))**%fitObj@b
  else
    fitObj@yhat <- drop(fitObj@X*%fitObj@b)
  fitObj}
```

构造函数的参数与 regr 类相同。现在，没有理由从头开始，因为我们已经知道如何创建 regr 对象。为了利用这一事实，首先使用 regr 构造函数创建 regr 对象，并使用 `as` 函数将其强制转换或提升为 regrFit 类。这种通用的 `as` 二进制形式如下：

```R
as(object, className)
```

