

select function.loop end
apply
...
 insert before %(printf("Found a loop\n"););
...
end

**图 3.32** insert 动作的简单示例。

select function.loop end
apply
...
 insert before %(printf("Found a loop at line %d!\n", *{[$loop.line]}););
...
end

**图 3.33** 向要插入的代码传递值的 insert 动作简单示例。

可以将 `aspect` 和/或连接点的数据传递给要插入的代码。图 3.33 展示了前一个示例的扩展，用于指示每个找到的循环的源代码行号。在此示例中，连接点 join 的 line 属性（`$loop.line`）作为 `[[]]` 之间的参数传递给插入的代码。织入过程会在每次执行 insert 语句时，将 `[$loop.line]` 替换为其实际值。同样，可以在要插入的代码段中使用 LARA 变量。

`Insert` 动作为在应用程序中添加/替换代码提供了一种强大的机制。指定代码插入策略的可能性是 LARA 最有用的概念之一。图 3.34 展示了一个 LARA aspect 示例，该 aspect 指定插入对函数 `QueryPerformanceCounter`⁶ 的调用，用于测量在 Windows 操作系统上运行的用 C 语言编写的应用程序的执行时间。请注意，该 `aspect` 需要插入 `#include`（第 5 行）、要使用的变量的声明（第 10 和 11 行）以及用于初始化和启动测量的代码（第 14 行中的 `select-apply`）和用于结束测量并输出结果的代码（第 24 行中的 `select-apply`）。此 aspect 提供了一种自动方案，用于修改带有类似于图 3.7 中所示并使用 `clock()` 函数⁷ 的调用的定时关注点的应用程序。图 3.34 中展示的代码可以轻松修改，以提供使用 `clock()` 的定时策略。

```
1. aspectdef InsertTiming
2.
3.   select file.first_header end
4.   apply
5.     insert after "#include <windows.h>";
6.   end
7.
8.   select function(name="main").first_stat end
9.   apply
10.    insert before %{ int64 freq, start, end, diff;
11.      long elapsedTime;%};
12.   end
13.
14.   select function(name="main").first_stat end
15.   apply
16.     insert before %{
17.       // get ticks per second
18.       QueryPerformanceFrequency((LARGE_INTEGER*)&freq);
19.       // start timer
20.       QueryPerformanceCounter((LARGE_INTEGER*)&start);
21.     %};
22.   end
23.
24.   select function(name="main").last_stat end
25.   apply
26.     insert after %{
27.       // stop timer
28.       QueryPerformanceCounter((LARGE_INTEGER*)&end);
29.
30.       printf("It took %d ticks", (end - start));
31.       printf("Freq %d\n", freq);
32.       elapsedTime = ((end - start) * 1000) / freq;
33.       printf("It took %d ms\n", elapsedTime);
34.     %};
35.   end
36. end
```

**图 3.34**
使用 LARA insert 动作在 Windows 中使用 QueryPerformanceCounter 包含用于测量应用程序执行时间（以 ms 为单位）的代码的示例。

## 3.5.3 EXEC 和 DEF 动作

在上一节中，我们介绍了 insert 动作，并展示了如何在应用程序的源代码中对代码进行插桩的策略编程。LARA 提供了其他类型的动作。exec 和 def 是两种用于通过使用编译器支持的特定代码转换来修改应用程序的动作。

exec 动作用于执行织入器定义的动作，例如特定的编译器通道（如循环展开）。def 动作用于修改某些应用程序工件，例如变量的数据类型。

图 3.35 展示了使用 exec 动作（第 6 行）来展开循环。在此示例中，aspect 指定按由变量“factor”表示的因子展开最内层且类型为 for 的循环。当应用于应用程序的源代码时，此 aspect 将展开所有尊重这些条件的循环。图 3.36 展示了一个更复杂的 aspect，当展开因子为零且所选循环具有大量迭代（在此情况下超过八次迭代）时，它会阻止最内层循环的完全展开。

```
1. aspectdef loopUnrollInnermost
2.   input factor end
3.
4.   select function.loop end
5.   apply
6.     $loop.exec Unroll(factor);
7.   end
8.
9.   condition
10.    $loop.is_innermost && $loop.type=="for"
11. end
```

**图 3.35**
使用 LARA exec 动作展开循环的示例。

```
1. aspectdef loopUnrollInnermost
2.   input factor end
3.
4.   select function.loop end
5.   apply
6.     if(factor == 0) {
7.       if($loop_num_iter < 8) { // limit fully loop unrolling
8.         $loop.exec Unroll(factor);
9.       } else {
10.        printf($loop.id+"no unroll");
11.      }
12.    } else {
13.      $loop.exec Unroll(factor);
14.    }
15.  end
16.
17.  condition
18.    $loop.is_innermost && $loop.type=="for"
19. end
```

**图 3.36**
使用 LARA exec 动作展开循环并使用规则决定是否展开的示例。

图 3.37 展示了一个示例，其中变量 z 被赋予 float 类型。此示例使用 def 动作，并意味着编译器中间表示（IR）的变化。

```
1. select var(name="z") end
2.   apply
3.     def type = "float";
4.   end
```

**图 3.37**
使用 LARA def 动作更改变量类型的示例。

```
call LoopUnrollInnermost(2);
```

**图 3.38** 调用语句示例。

## 3.5.4 调用 ASPECTS

LARA 提供了一种从 aspect 定义中调用 aspect 的机制，并可选择通过其输入和输出参数在它们之间共享数据。这增强了模块化和重用性。图 3.38 展示了一个简单示例，其中之前展示的 LoopUnrollInnermost aspect 之一以 2 作为其参数被调用。

在调用带有输出参数的 aspect 时，访问输出值的唯一方法是将标识符分配给调用，然后使用类似字段访问的语法。例如，在图 3.31 第 2 行的 call A.countFOR(loops); 中，标识符 A 用于表示 countFOR loops aspect 的特定调用。在第 3 行中使用 A.num_for_loops 允许在该特定调用中访问 num_for_loops 的值。

与调用相关的当前语义在 insert 和 exec/def 动作方面有所不同。insert 动作的结果在生成输出代码并将其输入到编译器之前，不会提供给后续的织入语句。也就是说，使用 insert 动作的代码修改在负责这些插入的织入过程中不会立即可见。

另一方面，exec/def 动作导致的更改在执行进入新 aspect 时即可用。我们在此展示一个示例，以说明 exec/def 动作的语义含义。之前在图 3.35 中展示的 aspect 展开最内层 for 循环。如果使用 factor = 0 应用该 aspect，我们将完全展开所有符合特定条件的循环。此 aspect 不会递归地完全展开循环，因为它只考虑应用程序中找到的原始最内层循环。递归调用此 aspect 将导致完全展开所有循环，而不考虑它们在嵌套循环结构中的原始位置。图 3.39 展示了一个可能的 aspect，它递归地展开程序中的所有循环。请注意第 23 行中 break 指令的使用，以防止展开因完全展开而不再存在的循环。图 3.40 说明了一个具有相同目标但使用迭代而非递归的 aspect。

## 3.5.5 执行外部工具

LARA 还允许从 aspect 中显式调用外部工具，并导入此类工具执行输出的数据，提供了一种透明的方式，以便在 LARA 级别使用反馈信息进行决策，并对特定工具流进行迭代。

图 3.41 展示了一个示例，该示例调用 Xilinx 后端工具，其输入为要综合、映射、布局和布线到特定目标 FPGA 的硬件的 VHDL 或 Verilog 描述。LARA aspect 还根据 opt 输入参数的值提供执行一个或多个工具的支持。

