
```
        }

    }

    return lval_err("Unbound Symbol '%s'", s);

}

lval* builtin_op(lval* e, lval* a, char* op) {

    for (int i = 0; i < a->count; i++) {

        if (a->cell[i]->type != LVAL_NUM) {

            return lval_err("'%s' expects a number", op);

        }

    }

    lval* x = lval_pop(a, 0);

    if (strcmp(op, "-") == 0 && a->count == 0) {

        x->num = -x->num;

    }

    while (a->count) {

        lval* y = lval_pop(a, 0);

        if (strcmp(op, "+") == 0) x->num += y->num;

        if (strcmp(op, "-") == 0) x->num -= y->num;

        if (strcmp(op, "*") == 0) x->num *= y->num;

        if (strcmp(op, "/") == 0) {

            if (y->num == 0) {

                x = lval_err("Division By Zero.");

                break;

            }

            x->num /= y->num;

        }

        lval_del(y);

    }

    lval_del(a);

    return x;

}

// Built-ins

lval* builtin_add(lval* e, lval* a) {

    return builtin_op(e, a, "+");

}

lval* builtin_sub(lval* e, lval* a) {

    return builtin_op(e, a, "-");

}

lval* builtin_mul(lval* e, lval* a) {

    return builtin_op(e, a, "*");

}

lval* builtin_div(lval* e, lval* a) {

    return builtin_op(e, a, "/");

}

```

```c

return builtin_op(e

for (int i = 0; i < v->count; i++) {

    if (v->cell[i] == LVAL_ERR) return lval_take(v, i);

}

if (v->count == 0) return v;

if (v->count == 1) return lval_take(v, 0);

}

```

```c

/* 评估后确保第一个元素是函数 */

lval* f = lval_pop(v, 0);

if (f->type != LVAL_FUN) {

    lval* err = lval_err;

    printf("Expression starts with incorrect type: %s\n", f->type);

    printf("Got %s, %s\n", f->type, lval_name(f->type));

    lval_del(f); lval_del(err);

    return err;

}

```

```c

/* 如果是，调用函数获取结果 */

lval* result = f->fun(e, v);

lval_del(f);

return result;

```

```c

lval* lval_eval(lenv* env, lval* v) {

    if (v->type == LVAL_SYM) {

        lval* x = len_get(env, v);

        lval_del(v);

        return x;

    }

    if (v->type == LVAL_SEXP) return lval_eval_sexpr(e, v);

    return v;

}

```

/* 读取 */

```c

lval* lval_read_num(mp_ast_t* t) {

    int errno = 0;

    long x = strtol(t->contents, NULL, 10);

    return errno == ERANGE ? lval_read_num(x) : lval_err("Invalid Number.");

}

return x;

```

/* 主函数 */

```c

int main(int argc, char** argv) {

    mpc_parser_t* Number = mpc_new("number");

    mpc_parser_t* Symbol = mpc_new("symbol");

    mpc_parser_t* Sexpr = mpc_new("sexpr");

    mpc_parser_t* Qexpr = mpc_new("qexpr");

    mpc_parser_t* Expr = mpc_new("expr");

    mpc_parser_t* Lispy = mpc_new("lispy");

}

```

```c

mpc_lang(MPCA_LANG_DEFAULT,

    number = /[0-9]+/;

    symbol = /[a-zA-Z0-9_-\\\|\*\<>!&]+/;

    sexpr = ('<sexpr>' expr);

    qexpr = ('<qexpr>' expr);

    expr = ('<expr>' <number> | <symbol> | <sexpr> | <qexpr>);

    lispy = ('<lispy>' expr /);

    Number, Symbol, Sexpr, Qexpr, Expr, Lispy);

    puts("Lispy Version 0.0.0.7");

    puts("Press Ctrl-c to Exit now");

    lenv* e = lenv_new();

    add_builtins(e);

    while (1) {

        char* input = readline("lispy> ");

        add_history(input);

        mpc_result_t r;

        if (mpc_parse(&r, "stdin", input, lval, &e)) {

            lval* x = lval_eval(e, lval_read(r.output));

            lval_print(x);

            lval_delete(x);

            mpc_delete(r.output);

        } else {

            mpc_delete(r.output);

            mpc_free(r);

        }

        free(input);

    }

```
```

## 额外奖励（Bonus）

-   创建一个处理报告错误的宏
-   创建一个处理报告错误的宏
-   创建一个处理报告错误的宏
-   创建一个处理报告错误的宏
-   某些函数输出的函数
-   重新定义处理报告错误的宏
-   创建一个处理报告错误的宏
-   创建一个 `exit` 这种 

# 第 12 章 什么是函数？

我们在 C 语言中使用许多函数，我们知道它们的样子，但并不确定它们到底是什么。这里有几种方式来思考它们。

一种思考函数的方式是它是想要执行的计算的描述。当你定义一个函数时，你是在说“当我使用这个名字时，我想让某事发生”。这是一个非常实用的函数想法。它是直观的，并且是对人类语言的比喻。我想的这种方式是函数被定义一次，但可以被多次调用。

另一种思考函数的方式是它是接收某些输入并产生输出的黑盒。这种想法与前者略有不同。它更具代数性，并且不讨论计算或命令。这个想法是一个数学概念，与特定的机器或语言无关。在某些情况下这非常有用。它允许我们在不考虑内部实现或如何计算的情况下思考函数。我们可以组合和组合函数，而不用担心出现微妙的问题。这是抽象的核心思想，使得不同层能够相互协作而不是冲突。这种想法的优点可能也是它的缺点。因为它没有提到任何计算，它没有处理现实世界中的许多问题：“这个函数运行需要多久？”这个函数高效吗？”它会修改程序的状态吗？如果是，如何修改？”

![](img/f0182debe747873c07b82d15dd58fde_110.png)

第三种方法是将函数视为部分计算。就像数学模型一样，它们可以接受某些输入。这些值在函数完成计算之前是需要的。这就是所谓的局部。但这种计算模型是由某些语言指定的计算，并且其输入是未绑定的。通过将一个齿轮放入之前旋转的机器中，完成了计算所需的全部。这些部分计算的输出本身是一个带有未知值的变量。

![](img/f0182debe747873c07b82d15dd58fde_111_0.png)

输出可以作为新函数的输入传递给任何现有的内置函数，就像任何其他函数一样

其他值并将其存储在环境中。

```
def add-together ({x y} (+ x y))
```

然后我们就可以通过名称来调用它。

```
add-together 10 20
```

## 函数类型 (Function Type)

为了将函数存储为 lval（左值），我们需要确切地思考它由什么组成。

使用之前的定义，一个函数应该由三部分组成。第一是形式参数列表，我们必须在评估函数之前对其进行绑定。第二部分是一个表示函数体的的 Q 表达式（Q-Expression）。最后，我们需要一个位置来存储赋值给形式参数的值。幸运的是，我们已经有了一个存储变量的结构，即环境（environment）。

我们将内置函数和定义的函数都存储在相同的类型 `LVAL_FUN` 下。这意味着我们在内部需要一种方法来区分它们。为了做到这一点，我们检查内置指针是否为 `NULL`。如果它**不为** `NULL`，我们就知道它是某个内置函数的 lval，否则它是一个用户函数。

```c
struct lval {
  int type;

  /* Basic */
  long num;
  char* err;
  char* opt;

  /* Function */
  builtin builtin;
  lenv* env;
  lval* formals;
  lval* body;

  /* Expression */
  int count;
  lval** cell;
};
```

我们将 `builtin` 字段从 `func` 重命名为 `builtin`。我们应该确保在代码中所有使用它的地方都进行更改。

我们还需要为用户定义的 lval 函数创建一个构造函数。在这里，我们为函数构建一个新环境，并将传入的形式参数和体的值赋值给它们。

```c
lval* lLambda(lval* formals, lval* body) {
  lval* v = malloc(sizeof(lval));
  v->type = LVAL_FUN;

  /* 将内置设为 Null */
  v->builtin = NULL;

  /* 构建新环境 */
  v->env = lenv_new();
  /* 设置形式参数和体 */
  v->formals = formals;
  v->body = body;
  return v;
}
```

每当我们更改 lval 类型时，都需要更新删除、复制和打印函数以处理这些变化。对于评估，我们需要更深层次的内容。

对于删除（Deletion）...

```c
case LVAL_FUN:
  if (v->builtin) {
    lenv_del(v->env);
    lval_del(v->formals);
    lval_del(v->body);
  }
  break;
```

对于拷贝（Copying）...

```c
case LVAL_FUN:
  if (v->builtin) {
    x->builtin = v->builtin;
  } else {
    x->builtin = NULL;
    x->env = lenv_copy(v->env);
    x->formals = lval_copy(v->formals);
    x->body = lval_copy(v->body);
  }
  break;
```

对于打印（Printing）...

```c
case LVAL_FUN:
  if (v->builtin) {
    printf("<builtin>");
  } else {
    printf("\\s"); lval_print(v->formals);
    putchar('('); lval_print(v->body); putchar(')');
  }
  break;
```

## Lambda 函数 (Lambda Function)

我们现在可以为 lambda 函数添加一个内置函数了。我们希望它接收符号列表作为输入，以及一个表示代码的列表。之后，它应该返回一个函数 lval。我们已经定义了一些内置函数，这一个将遵循相同的格式，就像 `def` 一样。我们进行一些错误检查以确保参数类型和数量是正确的（使用一些新定义的宏）。然后我们只需要从列表中弹出前两个参数，并将它们传递给之前定义的函数 `lval_lambda`。

```c
lval* builtin_lambda(lenv* e, lval* a) {
  /* 检查两个参数，每个都是 Q 表达式 */
  LASSERT_TYPE(a, a, 0, LV_QEXPR);
  LASSERT_TYPE(a, a, 1, LV_QEXPR);

  /* 检查 Q 表达式是否只包含符号 */
  for (int i = 0; i < a->cell[0]->count; i++) {
    LASSERT(a->cell[0]->cell[i]->type == VAL_SYM);
    /* 自定义非符号：获取 %s, 预期 %s。 */
    ltype_name(a->cell[0]->cell[i]->type), ltype_name(VAL_SYM));
  }

  /* 弹出前两个参数并将它们传递给 lval_lambda_ */
  lval* formals = lval_pop(a, 0);
  lval* body = lval_pop(a, 0);
  lval_del(a);

  return lval_lambda(formals, body);
}
```

## LASSERT_NUM 和 LASSERT_TYPE 从哪里来？

我冒昧改进了这一章的错误报告宏。这项任务在上一章的加分项中被提出。它让代码变得清晰得多，以至于很难忽略！

如果你计划自己完成这项任务，现在可能是这样做的好时机。否则，你可以查看本章的参考代码，看看我采取的方法，并将其整合到你的代码中。

## 父环境 (Parent Environment)

我们为函数提供了它们自己的环境。

（在这个环境中，我们为函数提供了了它们自己的环境。

*注：原文此处似乎存在逻辑上的重复，已根据语境翻译。*）

```
lval_del(a);
return lval_sexpr();
}
```

# 函数调用 (Function Calling)

我们需要编写在表达式被求值且函数 lval 被调用时运行的代码。

当这种函数类型是内置函数（builtin）时，我们可以像以前一样使用函数指针来调用它，但对于用户函数，我们需要进行一些特殊处理。我们需要将传入的每个参数绑定到 `forms` 字段中的每个符号上。这是在评估 `body` 字段时完成，使用 `env` 字段作为环境，并将调用环境作为父环境。

一个不包含错误检查的初步尝试可能如下：

```
lval lval_call(lval* env, lval* f, lval* a) {
/* 如果是内置函数则直接调用 */
if (f->builtin) return f->builtin(a);
/* 将参数赋值给每个形式参数 */
for (int i = 0; i < a->count; i++) {
lenv_put(f->env, f->formals->cell[i], a->cell[i]);
}
lval_del(a);
/* 设置环境 */
f->env->par = e;
/* 评估主体 */
return lval_add(lval_sexpr(), lval_copy(f->body));
}
```

但这并没有正确考虑到提供的参数数量与形式参数数量不符的情况。在这种情况下，程序会崩溃。

实际上，这是一个有趣的案例，并给了我们几个选择。我们可以在参数数量不时不直接抛出错误，但我们可以做一些更有趣的事情。当提供的参数过少时，我们可以绑定函数的前几个形式参数并返回它，留下剩余的未绑定。

这创建了一个被部分求值的函数，反映了我们之前关于函数是某种部分计算的观点。我们从一个接受两个参数的函数开始，传入一个参数，我们可以绑定第一个参数并返回一个新函数，其第一个形式参数已绑定，而第二个保持为空。
