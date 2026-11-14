

- 3. 循环报告。在应用程序终止之前，会生成并输出循环报告。

图 4.18 中的代码基于 blowfish 基准 [18,19]，展示了基于上述策略的插桩代码。

虽然监控 API 跟踪迭代次数和实例数，但手动插桩代码既费力又容易出错。我们可以使用图 4.19 中展示的 LARA 切面来自动化此过程，具体如下：

- 1. 第 2-8 行：选择每个源文件的第一条语句，并插入分析 API 的头文件。

- 2. 第 10-21 行：选择应用程序的所有循环及其对应的入口点。在每个循环语句之前，插入 monitor_count 调用以跟踪实例数，并插入迭代计数器的初始化语句。在循环体内插入循环计数递增，并在循环语句之后插入 monitor_avg API 调用以计算平均迭代次数（考虑循环之前的执行）。

- 3. 第 23-30 行：选择 main 函数的所有入口点，并插入 monitor_report() 调用以输出循环迭代次数和实例指标。

```
1. aspectdef lCount
2. select file.first_end
3. // add profile header
4. apply
5. if(first_insert before %{
6. #include <profiling.h>
7. %};
8. end
9.
10. select function.loop_entry end
11. apply
12. %{
13. %y key = $loop.key.replace(/\\/.g, "_");
14. %monitor_count("loop-instances", "[key]"); %};
15.
16. // $loop.insert before %{
17. %monitor_before %{
18. %monitor_insert after %{
19. %monitor_avg("loop-iterations", "[key]", COUNT_[key]); %};
20. end
21.
22. select function(name="main").exit end
23. // report monitor
24. apply
25. %{
26. %monitor_report("loop-iterations"); %};
27. %monitor_before
28. %monitor_insert before("loop-instances"); %};
29. end
30.
31. end
```

### 图 4.19 用于分析循环的 LARA 策略示例。

## 4.5.3 动态调用图

调用图通过表示不同程序模块（函数、子程序）之间的关系，为程序行为提供了一扇窗户。具体而言，调用图中的每个节点代表一个模块，边代表对模块的一次或多次调用。调用图可以在编译时（静态地）通过识别带有函数调用的语句来构建。它表示程序执行期间可能发生的所有调用的结构。在动态调用图的情况下，我们可以跟踪特定执行中调用的所有模块。具体而言，哪些模块被调用以及哪个模块触发了它们。动态调用图可以附加额外信息，例如其执行时间或其他指标。在本节中，我们专注于通过插桩代码生成动态调用图。插桩策略如下：

- 1. 分析 API 头文件。在每个源文件开头包含分析 API 头文件，以访问调用图监控函数。

- 2. 调用语句。在每个函数调用之前插入监控 API 调用（cgraph_task）。在此示例中，我们忽略所有系统调用。

- 3. 生成调用图。在应用程序终止之前，我们使用 cgraph_report 生成调用图。

让我们考虑基于 SHA 基准 [18,19] 的图 4.20 中的代码。它展示了基于先前策略的插桩代码，以加粗显示。我们可以使用图 4.21 中展示的 LARA 切面来自动化此过程，具体如下：

- 1. 第 3-8 行：选择每个源文件的第一条语句，并插入分析 API 的头文件。

- 2. 第 10-18 行：在每个调用之前插入 cgraph_task API 调用。cgraph_task API 调用接收两个参数：触发调用的函数名和被调用的函数名。我们添加一个条件，仅在调用不是系统调用时才跟踪该调用。

- 3. 第 20-25 行：选择 main 函数的所有退出点，并插入 cgraph_report() 调用以生成调用图。

## 4.5.4 分支频率

分支频率是另一项可用于确定热点的重要指标，特别是了解哪些分支被执行得最多，从而指导确定代码中哪个区域更适合优化的过程。与之前的示例一样，我们必须对代码进行插桩，在此情况下专注于条件结构，添加计数器，并使用具有代表性的数据集运行应用程序。我们的插桩策略如下：

```
#include <profiling.h>
void sha_final(SHA_INFO *sha_info) {
    if (count > 56) {
        memset(((BYTE *) &sha_info -> data) + count, 0, (64 - count));
        cgraph_task("sha_final","sha_transform");
        sha_transform(sha_info);
        sha_transform(sha_info);
        memset((&sha_info -> data),0,56);
    } else {
        memset((((BYTE *) &sha_info -> data) + count),0,(56 - count));
    }
    (sha_info -> data)[14] = hi_bit_count;
    (sha_info -> data)[15] = lo_bit_count;
    cgraph_task("sha_final","sha_transform");
    sha_transform(sha_info);
}
void sha_stream(SHA_INFO *sha_info, FILE *fin) {
    int i;
    BYTE data[8192U];
    cgraph_task("sha_stream","sha_init");
    sha_init(sha_info);
    while((i = fread(data,1,8192,fin)) > 0) {
        profile_graph_monitor("sha_stream","sha_update");
        sha_update(sha_info,data,i);
    }
    cgraph_task("sha_stream","sha_final");
    sha_final(sha_info);
}
void print_graph(SHA_INFO *sha_info) {
    printf("%08lX %08lX %08lX %08lX\n",
    (sha_info -> digest[0]),
    (sha_info -> digest[1]),(sha_info -> digest[2]),
    (sha_info -> digest[3]),(sha_info -> digest[4]);
}
```

### 图 4.20 基于 SHA 基准的代码示例。

- 1. 分析 API 头文件。在每个源文件开头包含分析 API 头文件，以访问分支频率监控函数；

- 2. 条件语句。为应用程序中的每个分支插入监控 API 调用（monitor_bfreq）。

- 3. 分支频率报告。就在应用程序终止之前，我们使用 report_bfreq API 调用生成分支频率报告。

我们现在考虑基于 Dijkstra 基准 [18,19] 的图 4.22 中的代码，它展示了基于先前策略的插桩代码，以加粗显示。

我们可以使用图 4.23 中展示的 LARA 切面来自动化此过程，具体如下：

- 1. 第 3–8 行：选择每个源文件的第一条语句，并插入分析 API 的头文件。

```
1. aspectdef CostGraph
2.
3.   // select the first (global) statement of the file
4.   select file.file first end
5.
6.   // add profile header
7.   apply
8.     profile_insert_before % (#include <profiling.h> %);
9.   end
10.
11.   // select all function calls
12.   select function.call end
13.   // add a monitor before each call
14.   apply
15.
16.     $call.parent_stmt.insert before % {
17.       cgraphTask("[[$function.name]]", "[$call.name]"); %};
18.   end
19.   condition !$call.is_sys end
20.
21.   // select last statement of the main function
22.   select function.end end
23.   // display call graph
24.   apply
25.     exit_insert_before % (cgraph_report()); %};
26.   end
27.   condition $function.name == "main" end
```

### 图 4.21 动态调用图的 LARA 策略示例。

- 2. 第 10–25 行：对于每个条件，选择“then”和“else”分支，并在每个分支内部插入 monitor_bfreq API。monitor_bfreq API 有两个参数：第一个是标识条件的键，第二个参数标识条件分支（then 或 else）。

- 3. 第 27–32 行：选择 main 函数的所有退出点，并插入 report_bfreq() 调用以输出条件被执行的总次数及其每条路径的频率。

## 4.5.5 堆内存

在开发没有自动垃圾回收的程序时，错误来源之一是堆内存管理。虽然 valgrind [6] 等复杂工具可以帮助调试潜在问题，但我们也可以使用自定义插桩来拦截对堆内存管理函数的调用，并监控其使用情况。我们跟踪堆内存使用情况的插桩策略如下：

- 1. 分析 API 头文件。在每个源文件开头包含分析 API 头文件，以访问堆监控函数。

- 2. 堆内存函数。拦截每个对 malloc、free 和 realloc 的调用，并分别将其替换为包装函数 profile_heap_malloc、profile_heap_free 和 profile_heap_realloc。

