

- 它在一定程度上保护我们程序员免受*功能主义*的影响——即痴迷于不断添加更多功能，而不是一件接一件地完成事情。如果我们写下想要实现的目标，我们会更直接地朝着这个目标努力，并且通常能更早地完成它。在测试中编写函数调用时，我们已经指定了计划实现的函数的接口。当我们为测试设置预期值时，我们就在说明我们函数的语义。因此，*测试是可编译的文档* [77]。测试可能无法告诉我们关于即将实现的函数和类的一切，但它所说的内容非常精确。文本文档可以比测试更详细、更易理解，但也可能比测试模糊得多。

- 如果我们在最终完成实现后才开始编写测试——比如说，在周五下午晚些时候——*我们不想看到它失败*。我们会使用良好的数据（无论这对所涉及的程序意味着什么）来编写测试，并尽量降低失败的风险。或者我们可能决定回家过周末，并发誓周一再测试它。

- 在高效工作的日子里，你想继续进行有趣且有挑战性的编程，而在那个时刻编写测试很可能会打断你的心流。你提前准备的测试越多，就能在心流中停留得越久。

出于这些原因，如果我们先编写测试，就会更诚实、更高效。

在TDD中，开发被组织为三个阶段的循环：编写测试、实现相应的代码，最后根据我们的软件理念对两者进行重构。如果我们的初始设计——在测试中体现——被证明行不通，或者会导致低效或不优雅的实现，我们可能会直接跳到重构，并根据新的知识调整测试，而不是痛苦地完成一个能通过测试的实现，然后在不久之后将其丢弃。不言而喻，验证部分实现需要暂时注释掉测试的部分内容。

- 在开始实现我们的逆函数及其测试之前，我们必须选择一个算法。我们可以在不同的直接求解器中选择：子矩阵行列式、分块算法、Gauss-Jordan方法，或带有或不带主元的LU分解。假设我们偏好带列主元的LU分解，因此有：

LU = PA，

其中L是单位下三角矩阵，U是上三角矩阵，P是置换矩阵。因此：

A = P⁻¹LU。

这意味着对于逆矩阵：

A⁻¹ = U⁻¹L⁻¹P. (A.1)

我们使用MTL4中的LU分解，实现下三角和上三角矩阵的求逆，并适当地组合它们。

```
=> c++11/inverse.cpp
```

- 现在，我们通过定义一个可逆矩阵并将其打印出来来开始我们的测试：

Click here to view code image

```
int main(int argc, char* argv[])
{
    const unsigned size=3;
    using Matrix = mtl::dense2D<double>; // Type from MTL4
    Matrix A(size, size);
    A=
        4, 1, 2,
        1, 5, 3,
        2, 6, 9;    // C++03
    cout << "A is:\n" << A;
```

- 为了以后的抽象，我们定义了类型Matrix和常量size。使用C++11，我们可以使用统一初始化来设置矩阵：

4. MTL4是用C++03编写的，我们仍然保持对该版本的向后兼容性。因此，必须通过像MTL_WITH_INITLIST这样的宏显式激活C++11特性。

Click here to view code image

```
Matrix A = {{4, 1, 2}, {1, 5, 3}, {2, 6, 9}}; // C++11
```

- 对于我们的实现，我们可以使用C++03，但为了减少与书中其余部分的差异，我们至少使用C++11。MTL4中的LU分解是原地执行的。为了不修改我们的原始矩阵，我们先将其复制到一个新矩阵中：

```
Matrix LU{A};
```

- 我们还为分解中计算的置换定义了一个向量：

```
mtl::dense_vector<unsigned> Pv(size);
```

- 这是LU分解的两个参数：

```
lu(LU, Pv);
```

- 出于我们的需求，将置换表示为矩阵更方便：

Click here to view code image

```
Matrix P{permutation(Pv)};
cout << "Permutation vector is " << Pv
<< "\nPermutation matrix is\n" << P;
```

- 这使我们可以通过矩阵乘积来表示行置换：

```
cout << "Permuted A is\n" << P * A;
```

- 我们现在定义一个单位矩阵，并从我们的原地分解中提取L和U：

Click here to view code image

```
Matrix I{matrix::identity(size, size)}, L{I +
strict_lower(LU)},
U{upper(LU)};
```

- 注意，L的单位对角线没有存储，测试时需要添加。它也可以隐式处理，但为了简单起见，我们不这么做。我们现在已经完成了准备工作，来到了第一个测试。一旦我们计算了U的逆（名为UI），它们的乘积必须是单位矩阵（近似）。L的逆也是如此：

Click here to view code image

```
constexpr double eps = 0.1;
Matrix UI(inverse_upper(U));
cout << "inverse (U) (permuted) is:\n" << UI
<< "UI * U is:\n" << Matrix(UI * U);
assert(one_norm(Matrix(UI * U - I)) < eps);
```

- 对非平凡数值计算结果进行相等性测试几乎肯定会失败。因此，我们使用矩阵差的范数作为标准。同样，L的逆（使用不同的函数）也进行了测试：

Click here to view code image

```
Matrix LI(inverse_lower(L));
cout << "inverse (L) (permuted) is:\n" << LI
<< "LI * L is:\n" << Matrix(LI * L);
assert(one_norm(Matrix(LI * L - I)) < eps);
```

- 这使我们能够计算A本身的逆并测试其正确性：

Click here to view code image

```
Matrix AI(UI * LI * P);
cout << "inverse (A) [UI * LI * P] is \n" << AI
<< "A * AI is \n" << Matrix(AI * A);
assert(one_norm(Matrix(AI * A - I)) < eps);
```

- 我们还用相同的标准检查我们的逆函数：

Click here to view code image

```
Matrix A_inverse(inverse(A));
cout << "inverse (A) is \n" << A_inverse
<< "A * AI is \n" << Matrix(A_inverse * A);
assert(one_norm(Matrix(A_inverse * A - I)) < eps);
```

- 在为计算的所有组件建立测试后，我们开始进行其实现。我们编程的第一个函数是上三角矩阵的求逆。该函数以稠密矩阵作为参数，并返回一个稠密矩阵：

Click here to view code image

```
Matrix inverse_upper(const Matrix& A) {
}
```

- 由于我们不需要输入矩阵的另一份副本，因此我们按引用传递它。参数不应被更改，因此我们可以将其作为`const`传递。constancy具有多个优点：

- 我们提高了程序的可靠性。作为`const`传递的参数保证不会更改；如果我们意外修改它们，编译器会告诉我们并中止编译。有一种方法可以删除constancy，但这只应作为最后手段，例如，用于与他人编写的过时库进行接口。你自己编写的一切都可以在不消除参数constancy的情况下实现。

- 当对象保证不会被更改时，编译器可以更好地优化。

- 对于引用，函数可以使用临时对象进行调用。非`const`引用需要将表达式存储到变量中并将变量传递给函数。另一个评论：人们可能会告诉你，将容器作为结果返回代价太高，使用引用更高效。这在原则上是正确的。目前，我们接受这种额外成本，并更关注清晰度和便利性。此外，现代编译器对返回值执行多种优化：容器中的数据可能会被移动而不是复制（参见§2.3.5中的移动语义），或者复制完全被省略（参见§2.3.5.3），因此你支付的比预期少，通常什么都不用付。

- 关于函数签名就说到这里；现在让我们将注意力转向函数体。我们的第一个任务是验证参数是否有效。显然，矩阵必须是方阵：

Click here to view code image

```
const unsigned n = num_rows(A);
if (num_cols(A) != n)
    throw "Matrix must be square";
```

- 行数在这个函数中需要用到多次，因此将其存储在一个变量中，嗯，常量中。另一个先决条件是矩阵的对角线上没有零元素。我们将此测试留给三角求解器。说到这一点，我们可以用一个

