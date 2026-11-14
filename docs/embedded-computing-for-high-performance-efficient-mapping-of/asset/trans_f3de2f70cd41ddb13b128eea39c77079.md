

![](img/55beb9162c0073b3a3d7b44f1d5873e8_132_0.png)

图 4.14 边缘检测 UTDS 基准的调用图（边上的标签标识每个被调用函数从调用函数被调用的次数）。

通过对代码进行插桩获得的任务图（TG）如图 4.15 所示。然而，我们未包含描述任务间及任务内部信息流的动态信息。可以看出，TG 明确显示了任务间的数据通信需求以及可以并行执行的任务。在此示例中，TG 显示两个 convolve2d 执行可以并行执行，这可以指导开发者，例如，将两个 convolve2d 函数实例映射到两个核上。

还可以提取的其他信息是生产者/消费者任务的访问模式，这可以是指导任务级流水线和支持任务间数据通信的硬件结构的重要信息（例如，根据访问模式，可以使用 FIFO 来通信数据）。

## 4.5 自定义分析示例

本节介绍了一些常用于嵌入式平台上下文中的代码分析自定义分析示例。所有示例都需要对应用程序进行插桩，以推导特定的动态指标。尽管应用程序的插桩可以手动完成，但我们在此强调使用 LARA 语言 [14,15] 来指定代码插桩策略，并使用基于这些策略生成代码修改的源到源编译器。

### 4.5.1 查找热点

加速应用程序执行的一个重要步骤是识别其热点，即花费大部分执行时间的代码区域，因此是优化的首选候选者。要识别热点，大多数开发者依赖于 GNU gprof 等免费可用工具，该工具提供关于程序每个模块花费执行时间的信息。GNU gcov 是另一个实用工具，在此情况下可用于呈现代码覆盖率结果。此类工具的功能有限，因为它们不提供选择要分析哪些代码区域和要忽略哪些区域的通用机制。不依赖分析工具，查找热点的一个简单策略是按如下方式手动插桩代码：

- 1. 分析 API 头文件。在每个源文件开头包含分析 API 头文件，以访问计时和报告函数。
- 2. 候选代码语句。在每个函数定义的开头和结尾插入计时调用，以计算相应的经过时间。我们仅对具有调用或循环的函数进行计时。
- 3. 计时报告。在应用程序终止之前，必须生成并输出计时报告。

![](img/55beb9162c0073b3a3d7b44f1d5873e8_133_0.png)

图 4.15
边缘检测 UT DSP 基准的任务图（TG）。

```
#include <profiling.h>
Boolean crc32file(char *name, DWORD *crc, long *charcnt) {
    timer_begin("crc32file");
    oldcrc2 = 0xFFFFFFFF; *charcnt = 0;
    if ((fin = fopen(name, "rb")) == NULL) {
        perror(name);
        timer_end("crc32file");
        return Error_;
    }
    while ((c=getc(fin))!=EOF) {
        ++charcnt;
        oldcrc2 = UPDC32(c, oldcrc2);
    }
    if (ferror(fin)) {
        perror(name);
        *charcnt = -1;
    }
    fclose(fin);
    *crc = ~oldcrc2;
    timer_end("crc32file");
    return Success_;
}
DWORD crc32buf(char *buf, size_t len) {
    timer_begin("crc32buf");
    oldcrc2 = 0xFFFFFFFF;
    oldcrc2 = UPDC32(*buf, oldcrc2);
    for ( ; len--; ++buf) {
        oldcrc2 = UPDC32(*buf, oldcrc2);
    }
    timer_end("crc32buf");
    return ~oldcrc2;
}
int multialign_arg(char *argv[]) {
    timer_begin("main");
    while(--argc > 0) {
        errors |= crc32file(*++argv, &crc, &charcnt);
        printf("%08lX %7ld %s\n", crc, charcnt, *argv);
    }
    timer_end("main");
    timer_report();
    return(errors != 0);
}
```

图 4.16 基于 CRC32 基准的代码。

例如，考虑图 4.16 中基于 CRC32 基准 [18,19] 的代码，我们在其中以粗体突出显示已插桩的语句。timer_begin、timer_end 和 timer_report 原语是专门开发的 API 的一部分，用于监控函数的执行时间和调用次数并提供计时报告。虽然我们的分析策略相对简单，但如果代码非常大且跨越多个源文件，手动插桩代码可能具有挑战性。我们的策略要求识别具有循环和函数调用的函数以及所有退出点（例如，return 语句）以插入 timer_end 原语。

```
1. aspectdef MyProfiler
2. // select the first (global) statement of the file
3. select file.first end
4. apply
5.
6. $first.insert before % #include <profiling.h> %;
7. end
8.
9. // select all function calls
10. select function end
11. apply
12. var loops = $function.pointcut("loop");
13. var calls = $function.pointcut("call");
14. if (loops.length > 0 || calls.length > 0) {
15. var entries = $function.pointcut("entry");
16. for (var i in entries) {
17. entries[i].insert before % timer_begin("[%[function.name]]"); %;
18. timer_begin("[%[function.name]]"); %;
19. }
20. var exits = $function.pointcut("exit");
21. for (var i in exits) {
22. exits[i].insert before % timer_end("[%[function.name]]"); %;
23. }
24. }
25. end
26. end
27. // select last statement of the main function
28. select function.exit end
29. apply
30. exit.insert before % timer_report(); %;
31. end
32. condition $function.name == "main" end
33. end
34. end
35. end
36. .
```

图 4.17 分析的 LARA 策略示例。

图 4.17 中展示的 LARA 切面基于我们的分析策略，通过对具有任意数量源文件的 C 应用程序进行插桩来自动化此分析过程，具体如下：

- 1. 第 3–6 行：选择每个源文件的第一条语句，并插入分析 API 的头文件。
- 2. 第 9–26 行：对于应用程序中的每个函数，我们识别它是否包含循环或函数调用。在此情况下，我们为该函数选择所有入口和退出语句，并分别插入相应的 `timer_begin` 和 `timer_end` 原语。
- 3. 第 29–33 行：选择 main 函数的所有退出点，并插入对 `timer_report()` 的调用。

### 4.5.2 循环指标

循环指标可以帮助确定哪些循环是优化的候选者：在硬件执行的上下文中，它们是将计算卸载到可重构硬件的首选候选者。在此分析中，我们希望识别程序中每个循环的平均迭代次数和每个循环的执行次数（实例数量）。与前一节一样，此代码分析需要对代码进行插桩以在执行期间收集关于循环的信息。

提取这两个循环指标的策略是按如下方式对程序中的每个循环进行插桩：

- 1. 分析 API 头文件。在每个源文件开头包含分析 API 头文件，以访问计时和报告函数。
- 2. 循环语句。在每个循环语句之前插入监控 API 调用（monitor_count）以计算其执行次数。此外，我们在循环体内插入一个计数器来监控每次循环执行的迭代次数，并使用 monitor_avg API 调用来跟踪平均值。

```c
#include <profiling.h>

void BF_set_key(BF_KEY *key, int len, unsigned char *data) {
    d = data;
    end = (data + len);
    memset(key, 0, sizeof(*key));
    int COUNT_BF_set_key_1 = 0;
    "BF_set_key_1");
    for (i = 0; i < 16 + 2; i += 4) {
        COUNT_BF_set_key_1++;
        rl = " (*(d++))";
    }
    monitor_avg("loop-iterations", "BF_set_key_1", COUNT_BF_set_key_1);
    in[0] = 0l;
    in[1] = 0l;
    monitor("loop-instances", "BF_set_key_2");
    int COUNT_BF_set_key_2 = 0;
    for (i = 0; i < 16 + 2; i += 2) {
        COUNT_BF_set_key_2++;
        P[2 * i] ^= encrypt(in, key);
        P[(2 * i) + 1] = in[1];
        p[1] = in[1];
    }
    monitor_avg("loop-iterations", "BF_set_key_2", COUNT_BF_set_key_2);
    p = (key->S);
    monitor("loop-instances", "BF_set_key_3");
    int COUNT_BF_set_key_3 = 0;
    for (i = 0; i < 4 + 256; i += 2) {
        COUNT_BF_set_key_3++;
        S[2 * i] ^= encrypt(in, key);
        S[(2 * i) + 1] = in[1];
        p[1] = in[1];
    }
    monitor_avg("loop-iterations", "BF_set_key_3", COUNT_BF_set_key_3);
}
```

图 4.18

来自 blowfish 基准的代码示例（粗体语句标识插桩插入的代码）。

