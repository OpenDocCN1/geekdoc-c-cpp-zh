
```c
while (1) {

char* input = readline("lispy");

add_history(input);

mpc_result_t r;

if (mpc_parse("stdin", input, Lispy, &r)) {

long result = eval(r.output);

printf("%lld\n", result);

mpc_ast_delete(r.output);

} else {

  mpc_err_print(r.error);

  mpc_err_delete(r.error);

}

free(input);

}

return 0;

}
```

# 加分项

- 编写一个递归函数计算树的叶节点数量。
- 编写一个递归函数计算树的分支数量。
- 编写一个递归函数计算节点的子节点数量。
- 如何使用 `strstr` 检查节点是否被标记为 `expr`？
- 如何使用 `strcmp` 检查节点是否有内容？
- 添加运算符 `%`，返回除余数。例如 `10 % 6` 是 `4`。
- 添加运算符 `^`，返回一个数字的次方。例如 `4^2` 是 `16`。
- 添加函数 `min`，返回最小数字。例如 `min 5 3` 是 `3`。
- 添加函数 `max`，返回最大数字。例如 `max 5 3` 是 `5`。
- 修改减法运算符 `-`，使其在接收一个参数时取反。

# 第 8 章：错误处理

## 崩溃

你们可能已经注意到上一章的问题。尝试输入以下：

```
Lispy Version 0.0.3

Press Ctrl+C to Exit

lispy / 10
```

哎呀。程序在尝试除以零时崩溃了。在开发期间程序崩溃是好的，但我们的最终程序应该永远不崩溃，并向用户解释发生了什么。

目前我们的程序可以产生错误，但在评估中还没有报告错误的功能。我们需要构建某种错误处理。在 C 中这样做可能很麻烦，但如果我们走在正确的轨道上，当系统变得复杂时会有回报。C 程序崩溃是生活的一部分。程序由于许多原因和不同的方式崩溃。你至少会看到一次。

C 中没有魔法。如果你遇到真正棘手的 Bug，不要放弃，直到你的眼睛血。利用这个机会正确学会使用 `gdb` 和 `valgrind`。这些将是你工具箱中的武器，在初始投入后将为你节省大量的时间和痛苦。

![](img/f182be74783c0.png)

## Lisp Value

在 C 中处理错误有很多方法，但在这种情况下，我倾向的方法是让表达式可能的结果。在 Lispy 中，表达式将返回一个数字或错误。例如 `* 2` 将返回数字，但 `/ 0` 将返回错误。

我们需要一个可以作为二者的数据结构。为了简单起见，我们将使用一个带有字段的 `struct` 来表示每个事物，一个特殊的 `type` 字段告诉我们哪些字段是有意义的。

我们将调用 `lval`，代表 Lisp Value。

```c
/* 定义 lval 结构 */

typedef struct {

    int type;

    long num;

    int err;

} lval;
```

## 枚举

你会注意到字段 `type` 和 `err` 的类型是 `int`。这意味着它们由单个整数表示。

我们选择 `int` 的原因是我们将为每个整数赋予意义以编码我们写的内容。例如，我们可以规定规则：“如果 `type` 是 `LVAL_NUM`，则结构就是数字；如果 `type` 是 `LVAL_ERR`，则结构就是错误。”这是一种简单有效的方法。

如果我们让代码跑偏将会变得越来越模糊。相反，我们使用分配了这些整数值的命名常量。这让读者知道为什么给 `LVAL_NUM` 或 `LVAL_ERR` 赋值，以及在这种语境下意味着什么。在 C 中，可以使用 `enum` 实现。

```c
/* 创建可能的 lval 类型枚举 */

enum { LVAL_NUM, LVAL_ERR };
```

枚举是变量的声明，在底层会自动分配整数常量。上面描述了我们如何为 `type` 字段声明枚举值。

我们还需要为 `error` 字段声明一个枚举。在我们特定的程序中有三种错误情况：除以零、未知运算符、或传递了无法用 `long` 内部表示的大数字。这些可以枚举如下：

```c
/* 创建可能的错误类型枚举 */

enum { LERR_DIV_ZERO, LERR_BAD_OP, LERR_BAD_NUM };
```

## Lisp 函数

我们的 `lval` 类型已经准备就绪。与之前的 `long` 类型不同，我们目前没有创建实例的方法。为了实现，我们声明两个函数来构造错误类型或数字类型的 `lval`。

```c
/* 创建一个新的数字类型 val */

lval lval_num(long x) {

    lval lval;

    lval.type = LVAL_NUM;

    lval.num = x;

    return lval;

}
```

```c
/* 创建一个新的错误类型 val */

lval lval_err(int x) {

    lval lval;

    lval.type = LVAL_ERR;

    lval.err = x;

    return lval;

}
```

```c
lval v;

v.type = LVAL_ERR;

v.err = x;

return v;
```

这些函数首先创建一个 lval v.，并在返回它之前对其字段进行赋值。

由于我们的打印函数可能是两种情况之一，我们不再能够仅仅使用 `printf` 来输出它。我们希望根据给定的 lval 类型有不同的行为。在 C 语言中，使用 `switch` 语句实现这一点的一种简洁方法。它接受一个值作为输入，并将其与其他已知值（称为 cases）进行比较。当值相等时，它会执行后续的代码直到遇到下一个 `break` 语句。

利用这种方法，我们构建了一个可以打印任何类型 lval 的函数：

```c
/* Print "lval" */

void print(lval v) {

  switch(v.type) {

  /* 如果类型是数字，则打印它 */

  /* 跳出 switch。 */

  case LVAL_NUM: printf("%d", v.num); break;

  /* 如果类型是错误 */

  case LVAL_ERR:

    if (v.err == LERR_DIV_ZERO) {

      printf("Error: Division By Zero!");

    }

    if (v.err == LERR_BAD_OP) {

      printf("Invalid Operator!");

    }

    if (v.err == LERR_BAD_NUM) {

      printf("Invalid Number!");

    }

    break;

  }

}

/* 打印 lval 并加上换行符 */

void lval_println(lval v) { lval_print(v); putchar("\n"); }
```

## 评估错误

现在我们已经知道如何处理 lval 类型，我们需要修改评估函数以使用它而不是 `long`。

除了修改函数签名外，我们还需要修改函数，以便它们在遇到错误输入或数字输入时能够正常工作。在我们的 `eval_op` 函数中，如果遇到遇到错误，我们应该立即返回它，并且只有当两个参数都是数字时才进行计算。我们应该修改代码以返回错误，而不是尝试除零。这将修复在本章开头描述的崩溃问题。

```c
lval eval_op(lval x, char* op, lval y) {

  /* 如果任一个是错误则返回它 */

  if (x.type == LVAL_ERR) { return x; }

  if (y.type == LVAL_ERR) { return y; }

  /* 否则对数值进行数学运算 */

  if (strcmp(op, "+") == 0) { return lval_num(x.num + y.num); }

  if (strcmp(op, "-") == 0) { return lval_num(x.num - y.num); }

  if (strcmp(op, "*") == 0) { return lval_num(x.num * y.num); }

  /* 如果第二个操作数为零则返回错误。 */

  return y.num == 0

    ? lval_err(LERR_DIV_ZERO)

    : lval_num(x.num / y.num);

  return lval_err(LERR_BAD_OP);

}
```

## 什么是 ? ？ 用于除法检查第二个参数是否为零我们使用

你会注意到问号符号 `?`。这被称为三元运算符，它允许你在一行内编写条件表达式。
它的工作原理类似于：`<condition> ? <then> : else`。换句话说，如果条件为真，它返回后面的内容，否则返回另一个内容。

有些人不喜欢这种三元运算符，因为他们认为它会让代码不清晰。如果你熟悉三元运算符，最初可能会觉得用起来很别扭；但一旦你学会了它，很少会有问题。

我们需要对 `eval` 函数进行类似的处理。在这种情况下，我们已经定义了 `eval_op` 来健壮地处理错误，我们只需要在数字转换中添加错误条件。

在这种情况下，我们使用 `strtol` 函数将字符串转换为 `long`。这允许我们检查特殊变量 `errno` 以确保转换正确进行。这比之前使用 `atoi` 的方法是一种更健壮的转换方式。

```c
lval eval(mp_ast_t* t) {

  if (strcmp(t->tag, "number")) {

    /* 检查转换过程中是否存在错误 */

    errno = 0;

    long x = strtol(t->num, NULL, 10);

    return errno == ERANGE ? lval_num(x) : lval_err(LERR_BAD_NUM);

  }

  char* op = t->children[1]->contents;

  lval x = eval(t->children[2]);

  int i = 0;

  while (strcmp(t->children[i]->tag, "exp") != 0) {

    x = eval_op(x, op, eval(t->children[i]));

    i++;

  }

  return x;

}
```

最后的一一步是修改我们打印评估结果的方式，使用我们新定义的函数，该函数可以打印任何类型的 lval。

```c
lval result = eval(r.output);

lval_println(result);

mpc_ast_delete(r.output);
```

我们完成了！运行这个新程序，并确保在除零时不会发生崩溃。

```c
",nNumber, Operator, Expr, Lispy);

puts("Lispy Version 0.0.0.4");

puts("Press Ctrl+c to Exit");

while (1) {

  char* input = readline("Lispy > ");

  add_history(input);

  mpc_result_t r;

  if (mpc_parse(input, lispy, &r)) {

    lval result = eval(r.output);

    lval_print(result);

    mpc_ast_delete(r.output);

  } else {

    mpc_err_print(r.error);

    mpc_err_delete(r.error);

  }

  free(input);

}

mpc_cleanup(&, Number, Operator, Expr, Lispy);

return 0;
```

# 额外奖励

- 使用 gdb 运行上一章的代码并让其崩溃。看看发生了什么。
- 如何给枚举（enum）命名？
- 什么是联合体（union）数据类型？它们是如何工作的？
- 你否修改 `lval` 的定义，使其使用联合体代替结构体（struct）？
- 过度使用联合体而不是结构体的优点是什么？
- 扩展解析和求值以支持取模运算符 `%`
- 扩展解析和求值以支持使用 `double` 字段的数字类型

# S-表达式 • 第 9 章

## 列表与 Lisp

Lisp 以数据和代码之间生动的区分而闻名。它们使用相同的结构来表示两者。这使得它们能够完成其他语言无法完成的许多强大功能。如果我们想要实现我们的编程语言，就必须将读取输入的过程与评估我们存储的输入的过程分开。

本章的最终结果在行为上与上一章略有不同。这是因为我们将花费时间改变某些内部实现。这是一个良好的重构，会让我们以后的工作变得轻松一些。就像准备饭一样，仅仅因为我们没有把食物放在盘子里，并不意味着我们在浪费时间。有时候，期待的过程比结果更好！

![](img/f0182debe7478735c07b82d15dd58fde_55_0.png)

为了存储程序，我们需要创建一个内部结构，该结构由数字、符号和其他列表递归地构建。在 Lisp 中，这种结构通常被称为 S-表达式（S-Expression），代表“符号表达式”（Symbolic Expression）。我们将扩展本地结构以能够表示它。S-表达式的求值是 Lisp 的典型行为，也是我们迄为止习惯的。要评估一个 S-表达式，我们查看列表中的第一个项，并将其作为运算符。我们查看列表中所有其他项，并将它们作为操作数以获得结果。

通过引入 S-表达式，我们终于进入了 Lisp 的世界。

## 指针

在 C 语言中，如果不正确处理指针，就探索列表的概念。指针是 C 语言中著名的被误解的方面。它们很难教，但在概念上又非常简单；它们伴随着许多新术语，而且没有明确的用例。这使得它们看起来比实际要狰狞得多。幸运的是，我们有两个理想的用例，这两者在 C 语言中都极其典型，并且很可能成为你 90% 时间里使用指针的方式。

我们在 C 中需要指针的原因是函数调用的工作方式。当你在 C 中调用函数时，参数总是通过值传递传递的。这意味着它们的副本会被传递给你调用的函数。这对于 `int`、`long`、`char` 以及偶尔的用户定义的结构体类型（如 `lval`）都是如此。大部分情况下很好，但偶尔会引起问题。

当我们有一个包含许多其他想要传递的大型结构体时，就会出现常见问题。每当我们调用函数时，必须创建另一个副本。突然，仅仅为了调用函数而需要复制的数据量可能会变得巨大！

第二个问题是，如果我们定义一个结构体，它是固定大小的。它有有限的字段，而且每个字段必须是一个自身大小受限的结构体。如果我想用一个列表来调用函数，其中项的数量随调用而变化，我显然不能使用结构体来增长和缩小。

为了解决这些问题，C 的开发者（或某位……）想出了一个好主意。他们将计算机内存想象成一个单一列表。（此处原文中重复的句子已按要求处理）。

有一个对应的（且仅有一个对应的）`free`。如果能始终确保这一点，程序就能处理好 U-Store-It。
把堆（Heap）想象成一个巨大的 U-Store-It。我们可以通过 `malloc` 召唤接待员并请求一些箱子。有了这些箱子，我们可以随心所欲地使用，而且我们知道无论工地变得多么混乱，它们都会一直存在。我们可以在 U-Store-It 和工地之间取送物品。这对于存储我们一段时间后才需要取回的和大型对象非常有用。唯一的问题是，当我们完成后，需要再次通过 `free` 召唤接待员。
否则，很快我们就请求了所有的箱子，没有空间，并欠下了巨额账单。

## 解析表达式 (Parsing Expressions)

由于我们现在是在思考 S 表达式（S-Expressions）而不是波兰表示法，因此我们需要更新解析器。S 表达式的语法非常简单。它只是括号内的若干个表达式，其中表达式可以是数字、运算符或 S 表达式。我们可以修改现有的解析器规则来反映这一点。这是为了预留以后添加更多运算符和函数的空间。

```
mpc_parser* Number = mpc_new("number");

mpc_parser* Symbol = mpc_new("symbol");

mpc_parser* Sepr = mpc_new("sepr");

mpc_parser* Expr = mpc_new("expr");

mpc_parser* Lispy = mpc_new("lispy");
```

```
mpca_lang(MPCA_LANG_DEFAULT,

number : /[0-9]+/ / \ \

symbol : /^[a-zA-Z_]+/ / / \

sepr   : /' <expr>*' / / \

expr   : /<number> <symbol> <sepr>* / / \

lispy  : /<expr>* / / \

,

Number, Symbol, Sepr, Expr, Lispy);
```

我们还应该记得清理这些规则。

```
mpc_cleanup(5, Number, Sepr, Expr, Lispy);
```

## 表达式结构 (Expression Structure)

我们需要一种方法将 S 表达式存储为 `lval`。这意味着我们还需要存储存储符号（Symbols）和数字（Numbers）。我们将向枚举（enum）中添加两种新的 `lval` 类型。第一个是 `LVAL_SYM`，我们将用它表示如 `+` 等运算符。第二种新类型是 `LVAL_SXPR`，我们将用它表示 S 表达式。

```
enum { LVAL_ERR, LVAL_NUM, LVAL_SYM, LVAL_SXPPR };
```
