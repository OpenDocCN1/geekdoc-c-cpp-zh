
`mul({vec, I, J}, K) when is_number(K) ->`

`{vec, K*I, K*J}.`

`as_string({vec, I, J}) ->`

`lists:flatten(io_lib:format("~w,~w", [I, J])).`

模块由属性和函数声明组成。`module` 提供模块名，该名称必须与包含模块的文件名一致。第二个属性 `export` 列出了模块客户端可用的函数；任何未导出的函数都是模块私有的。导出列表中的函数带有其元数（参数个数）给出的，因为 Erlang 区分同名但元数不同的函数。

编译后，我们可以像使用任何现有的脚本一样使用我们的模块：

```erlang
% 在作为脚本运行时，第一行会被忽略

main() ->

    U = vectors:create(3, 4),

    V = vectors:create(-5, 10),

    {vec, 3, 4} = U,

    {vec, -5, 10} = V,

    {vec, 15, 20} = vectors:mul(U,V),

    5.0 = vectors:magnitude(U),

    "~2,14>" = vectors:as_string(vectors:add(U,V)).
```

我们将向量表示为一个元组，其第一个元素是一个指示其“类型”的原子。虽然存在其他表示方法，但这种常见且符合习惯的技巧将我们很好地引入模式匹配的世界，我们现在正转向这里。

## 10.3 匹配

与许多语言中的赋值语句不同，Erlang 变量通过模式匹配进行绑定。一旦绑定，它们就无法重新绑定。我们可以在 REPL 中看到这一点。

### 198 编程语言探索

```bash
$ erl

1> X = 10.

10

2> X = 20.

** exception error: no match of right hand side value 20

3> X = 10.

10
```

我们的第一个输入匹配了未绑定的变量 `X` 并进行绑定，将 `X` 绑定到 `10`。第二次尝试将 `10`（`X` 已经绑定的值）与 `20` 匹配，这失败了。我们的第三次匹配成功了，它与 `10` 匹配成功。

Erlang 中的模式匹配可以一次绑定多个变量：

```erlang
% 在作为脚本运行时，第一行会被忽略

main() ->

 S={student, name="Alice", {scores, [93,100,81,88]}},

#### 模式匹配绑定两个变量

{name, Name}, {scores, [|Midterm|_]}} = S,

#### 断言

100 = Midterm,

"Alice" = Name.
```

我们使用了特殊变量 `_`，它不绑定到任何内容，并匹配所有内容。它是模式中目前不关心的位置的完美占位符。

匹配不仅发生在匹配运算符 (`=`) 中，也发生在函数定义和 `case` 表达式中。这些结构有多个子句，用分号分隔。Erlang 按子句的顺序执行匹配，一旦找到匹配项就会采取行动：

```erlang
% 函数句中的模式匹配

area({circle, R}) -> math:pi() * R * R;

area({rectangle, W, L}) -> W * L.

% case 表达式中的模式匹配

roll() ->

case {rand:uniform(6), rand:uniform(6)} of

{D, D} -> "You rolled doubles", D+D;

{X1, Y1} -> "Unrolling roll", X1+Y1

end.
```

```erlang
main() ->

 40 = area({rectangle, 8, 5}),

 {_, _} = roll().
```

```erlang
我们可能需要编写用于匹配的代码，这将非常方便。判断一个值是否在 2000 到 32000 之间似乎需要 30,000 个子句。如果我们的项是特定类型，我们无法直接表示成功的匹配，因此 Erlang 使用守卫（guards）。我们将通过一个例子来说说明：
```

```erlang
%% 返回 X 是否为 (1) Y 或 (2) 是否在列表 Y 中
at (X, Y) when is_list(Y) -> lists:member(X, Y);
at (X, Y) -> X := Y.
```

```erlang
grade(Score) when Score >= 90 -> 'A';
grade(Score) when Score >= 80 -> 'B';
grade(Score) when Score >= 70 -> 'C';
grade(Score) when Score >= 60 -> 'D';
grade(_) -> 'F'.
```

```erlang
main() ->
['C','A','F','B','D'] = [grade(S) || S <- [71,99,77,80,60]];
true = at(dog, dog),
true = at(rat, cat),
false = at(bat, dog).
```

产生布尔值的表达式允许在守卫中使用；守卫必须没有副作用。Erlang 用户指南列出了允许的表达式列表。Erlang 为那些不需要模式匹配但需要守卫的情况提供了 `if` 表达式：

（此处代码块为空，未翻译）

## 10.4 消息传递

Erlang 最初是为了解决电话问题而创建的，因此从一开始就是为并发设计的。电话应用需要大规模的扩展和高可靠性。共享内存的线程以及共享单个处理器的协程可能无法很好地满足这些需求，而 Erlang 的进程拥有自己的内存，并通过消息传递进行协作。进程异步地发送消息到其他进程的邮箱；这里没有锁。由于进程没有内存，它们崩溃时不会留下系统不一致的状态。这有助于 Erlang 的设计者以及他们的虚拟机 BEAM 实现轻量级进程、快速启动和关闭，允许成千上万个进程并发运行。Erlang 的进程具有两个特性：主进程产生新进程并立即等待消息。内置函数 `spawn()` 返回进程标识符（pid），即执行进程的 pid。主进程在构造时将 pid 传递给每个素数检查进程。每个素数检查器检查要打印的数字，合数则返回 false。主进程在完成之前等待打印器的 999 条消息以处理每个值。

```erlang
% 在作为脚本运行时，第一行会被忽略
main() ->
    spawn(fun -> ! "Hello" end),
    receive
        S -> io:format("-s~n", [S])
    end.
```

该脚本说明了进程设计的四个元素：

- p 产生 q，q 与 p 并发运行。
- 当 p 向 q 发送消息时，在 q 的邮箱中等待接收。
- Erlang 应用在主进程结束时终止，即使有数百个进程仍在运行；因此，主进程使用 `receive` 表达式等待某种“完成”信号是常见的。

我们的下一个脚本说明了这一点。它启动1000个进程来检查 2..1000 范围内的特定数字是否为素数，并负责打印到标准输出：

```erlang
% 在作为脚本运行时，第一行会被忽略
main() ->
    Max = 1000,
    Printer = spawn(printer, print_server, [self()]),
    lists:foreach(
        fun (N) ->
            spawn(prime_checker, is_prime, [N, Printer]),
            lists:seq(2, Max),
            wait(Max-1)
        end),
    wait() -> io:format("-n~n");
    wait(N) -> receive -> wait(N-1) end.
```

> 寻找素数是对并发的一次有趣的探索，但在实践中，该任务有更合适的顺序解决方案。这种方案特别原始且低效。

### Erlang 201

内置函数 `spawn(module, function, args)` 创建一个进程异步运行 `module:function(args)`，并立即返回该新进程的 pid。我们在构造时将打印器的 pid 传递给每个素数检查进程。每个素数检查器检查数字，我们用主进程set的 pid 构建打印器进程，这样打印器就可以向主进程发送消息来处理每个值。主进程在结束之前等待打印器的 999 条消息。

素数检查器本身也很有趣，因为我们有机会来说明递归。

```erlang
-module(prime_checker).
-export([is_prime/2]).

is_prime(N, Observer) ->
  fun Check(D) ->
    if
      D * D > N -> % 没有更多因数
        Observer ! N;
      N rem D == 0 -> % 合数
        Observer ! false;
      true -> % 继续寻找
        Check(D+1)
    end
  ().
```

素数检查函数说明了使用尾递归实现“循环”的典型方法。检查 2..√N 可能的因数，通知观察进程我们的值（如果是素数）或非素数的指示（false）。我们的打印进程向标准输出重复整数，通知观察者是否打印了值。

```erlang
-module(printer).
-export([print_server/1]).

print_server(Observer) ->
  receive
    N when is_integer(N) ->
      io:format("-p~n", [N]);
      Observer ! true;
    ->
      Observer ! false
  end,
print_server(Observer).
```

不要依赖进程完成的顺序：该脚本的一次运行开始于：23 179 181 191 193 197 71 73 21 323 227 229 239 233 241 43 25 261 257 263 269 67 277 271 281 283 79 101 103 83 29 307 311 313 317 107 109 33 5 7 13 17 19 113 2 ... 以及其他运行是乱序的。

> ⁴ 我们对发送什么消息并不十分美观；清理这些代码对读者来说是一个很好的练习，研究更符合习惯的等待一组进程完成的方法也是如此！
> ⁵ 因为闭包的内部函数 Check 是递归的，所以我们必须给它起一个名字。

### 202 编程语言探索

Erlang 允许如下使用 `receive` 表达式。它检查邮箱中的第一条消息（消息按到达顺序队列），并尝试按顺序与每个 `receive` 模式匹配。就像 `case` 表达式和函数一样，`receive` 模式也可以带有守卫（guards）。如果找到带有真守卫的匹配模式，则评估相应的体以产生 `receive` 表达式的结果。如果没有找到，则考虑邮箱中的第二条消息（以此此类推，直到检查整个邮箱）。如果没有消息符合条件，`receive` 表达式将阻塞，直到有合适的消息到达——或者直到超时（如果提供了超时，我们很快就会看到）。

让我们重新回顾 Java 章中的厨师和客户模拟，并为了增加多样性进行一些修改。每个客户吃 10 次餐后离开。客户在订单池中下单；厨师从池中获取订单。厨师处理订单并将准备好的餐点直接送送到客户的桌上。如果客户没有得到及时的服务，他们就会离开并在稍后回来，那时他们会发现食物是凉的。

在我们的模拟中，池不是共享的全局数据结构，而本身本身就是一个进程。客户通过向池发送消息 `{place, {pid, food}}` 来下单，其中 `pid` 是客户的进程 ID。进程频繁发送自己的 `pid` 以便被回调。一个准备好工作的厨师会向池发送消息 `{ready, pid}`；如果有任何已放置订单，池会向厨师发送消息 `{prepare, {customerpid, food}}`，指示厨师为客户准备餐点。准备好餐点后，厨师向客户发送消息 `{serve, meal}`。图 10.1 以图片形式描述了这一场景。

![](img/2cd8452ff5a372a7459559ad1d0834e4_220_0.png)

图 10.1 Erlang 餐厅模拟中的消息传递

我们的脚本创建了订单池，并在创建每个客户和厨师进程时将其 `pid` 传递给它们。在每个进程启动后，脚本会睡眠三分钟，模拟餐厅营业的时间。模拟并没有等待 actor 的完成进程，而是利用了主进程一直留在脚本应用程序中的这一事实，整个过程将持续下去。

```erlang
% 使用脚本运行时，会忽略第一行

main() -
  Orders = spawn(order_pool, run, []),
  [spawn(cook, run, [Name, Orders]) || Name <- ["Aly","Rob","Chi"]],
  [spawn(customer, run, [Name, Orders]) || Name <- ["Xia","Ann","Bo",
"Rai","Ali","Kat","Esche","Sen","Ami","Lina","Ara","Zuri"]]],
  timer:sleep(18000).
```

> 如果从具有真守卫，则可以在没有守卫的情况下工作。

### Erlang 203

现在来看订单池。池可以随时接受客户的订单，并将订单“添加”到池中。Erlang 是一种函数式语言，所以“添加”意味着带有一个新池进行递归，就像在原始池后面追加新订单一样。池还会接受厨师取订单的请求，但仅在存在订单时，因此我们使用了守卫。如果订单就绪，池会向厨师发送要准备的食物消息，“出队”最旧的订单。

```erlang
-module(order_pool).
-export([Orders]).

run(Orders) ->
  receive
    {place, Order} ->
      lists:append(Orders, [Order]);
    {ready, Cook} when length(Orders) > 0 ->
      {prepare, had(Orders)},
      run(t1(Orders))
  end.
```

厨师在准备就绪时会反复向订单池发送消息，然后等待接收订单消息。厨师通过内置函数 `self` 传递其 `pid`。厨师接收包含食物和下单客户 `pid` 的元组作为订单。准备好后，厨师向客户发送 `{serve, meal}`。

```erlang
-module(cook).
-export([run/2]).

run(Name, Orders) ->
  receive
    {ready, self()} ->
      {prepare, {Customer, Order}} ->
        Meal = cook(Name, Order),
        Customer ! {serve, Meal},
        run(Name, Orders)
  end.

cook(Name, Food) ->
  io:format("-s is cooking -n", [Name, Food]),
  timer:sleep(rand:uniform(5000)),
  Food ++ " cooked by " ++ Name.
```

客户吃 10 次餐。为了简单起见，客户只负责下单。他们下单，然后等待厨师发送准备好的餐点。`receive` 表达式的 `after` 部分使得这变成了定时等待：如果在超时时间内没有收到消息，则执行 `after` 子句并终止。无论客户得到食物还是放弃，都会循环等待下一餐。

```erlang
-module(customer).
-export([run/2]).

run(Name, Orders) ->
  Orders ! {place, self(), "soup"},
  eat(Name, Orders, 10).

eat(Name, _, 0) ->
  io:format("-s going -n", [Name]);
eat(Name, Orders, Times) ->
  receive
    {serve, Meal} ->
      io:format("-s eating -n", [Name, Meal]),
      timer:sleep(rand:uniform(5000)),
      Orders ! {place, self(), "soup"},
      eat(Name, Orders, Times - 1)
    after 7000 ->
      io:format("-s waiting too long -n", [Name]),
      timer:sleep(rand:uniform(5000)),
      eat(Name, Orders)
  end.
```

到为止的示例强调了并发 Erlang 哲学的三个方面：

- 进程通过将数据结构传递给递归调用来管理状态。
- 进程通信是数据驱动而非过程驱动。在我们的示例中，厨师并不对客户调用 `serve`。通信中使用的唯一动词是 `!` 和 `receive`。进程所需的任何操作（如 `place`, `order`, `cook`）都是通过检查消息和模式匹配决定的。然而在生产级应用中，你可能希望创建特定的函数以防止进程感知细节。这样做允许更改消息格式而不破坏 actor 之间的高层交互。
- 我们没有使用任何进程池；我们根据需要创建进程，并让 Erlang 担心进程过多以及如何调度。
