
This tool allows the developer to integrate the C# language capabilities in his own application. The application domains are quite large, like:

- The integration of a scripting language for automatizing your application,
- On the fly compilation of custom module developed by the user

Indeed the integration of a programming language could be a great benefit for the user and opens field of application to another level with automations capabilities.

Roslyn provide to the developer the possibility to integrate a robust and customizable language for the programming and the automation of the developed software.

![](img/3d310cc066dda6e2dfa67a650614076f_288_0.png)

## Chapter 10. APPLICATION PERFORMANCES IMPROVEMENT

The performances are often a critical point in many software development projects. In this chapter we will review, how to identify the bottlenecks inside the source code using the built-in Visual studio tools and afterward review a Benchmark dedicated tool (able to produce advanced reports).

We will finally review handy techniques and tips for producing high performances C# source from the start.

But do not forget performances issues come often from an inappropriate choice in the architecture of the software (especially for a desktop, local application).

If you encounter performances issues of this type do not hesitate to modify the architecture planned as soon as the issue is identified: as soon the architecture will be fixed (and modified) the less time you will spend to try to fix or to patch a dodgy program architecture.

In the other cases, the developer can use a simple method for the implementation of a performance enhancement process.

Here is the simple cycle the developer can follow for achieving this goal.

![](img/3d310cc066dda6e2dfa67a650614076f_289_0.png)

(Performance enhancement process)

### 10.1 USE VISUAL STUDIO RUNNING ANALYSIS TOOLS

Visual Studio 2019 is an awesome tool for the real time performance visualization of a running program.

If the “Diagnostic Tools” window is not display on your Visual Studio configuration you can select the menu:

```
Debug/Windows/Diagnostic Tools.
```

The “Diagnostic tools” view is open (by default) each time the program is executed from the Visual Studio environment (the window is displayed at each run session).

This view provides real time indicators about the chronology of the execution, the CPU usage of the program process, the system events triggered, and the amount of memory used by the program as you can see on the picture below (figure 1).

![](img/3d310cc066dda6e2dfa67a650614076f_290_0.png)

(figure 1)

All of these indicators can be used by the developer to identify if a specific methods or objects have an abnormal consumption of CPU or memory when it is loaded or executed. This tool provides a good view for the identification of source code who have to be optimized fixed or refactored.

It also can help the developer to choose a pertinent and appropriate architecture regarding those results (and change it, if it is needed).

You can view the “CPU usage” by methods by enabling it; through the “CPU Usage” tab as shown (figure 2) below.

![](img/3d310cc066dda6e2dfa67a650614076f_291_0.png)

(figure 2)

You can also use the “Performance Profiler” (Analyze/Performance Profiler) for analyzing the performances (CPU usage, memory ...) of your running application in live.

There is a limitation to the use of this tool, the “Performance analyzer” analyses only one indicator per session of profiling, if you need CPU usage and memory you have to perform two analysis.

"Performance Profiler" can generate a report: a ".diagsession" file.

The ".diagsession" file can be saved on disk by right clicking on the report tab and select "Save Report*.diagsession" as shown below (figure 3).

![](img/3d310cc066dda6e2dfa67a650614076f_292_0.png)

Visual Studio 2019 provides amazing tools for performances analysis and in many cases, it will cover all your needs in that matter.

The development of desktop application does not require (generally) much more indicators of performance than the ones provided with the Visual Studio 2019 tools (This subject is less important for a desktop application than it is for a web application).

### 10.2 .NET CORE 3 PERFORMANCES BENCHMARKS

Visual Studio 2019 performance analysis tool are efficient for the developer but if your project requires detailed reporting on the performances or studies on performances enhancement evolution, it will not be the only tool you will need to use.

The performance benchmarking of .NET Core 3 application can be done effectively by the use of a specialized library:

### BenchmarkDotNet.

This package can report (console, html, csv file) allowing the accurate evaluation of the weight (in time perspective) of each object methods you use. It can also be configured to analyze the memory usage and the garbage collector status.

This library is available under NuGet packaging:

![](img/3d310cc066dda6e2dfa67a650614076f_293_0.png)

BenchmarkDotNet is used for accurately measuring the time spend by each piece of code (which you have marked with a dedicated attribute).

Here is sample code calculating the factorial of a number, and using BenchmarkDotNet for measuring the time spent for the execution of the methods.

```
using BenchmarkDotNet;
using System.Math;

public class BenchmarkFact
{
    [Benchmark]
    public int calculateFactorial(int i)
    {
        ...
    }
    static void Main()
    {
        BenchmarkRunner.Run<BenchmarkFact>();
        Console.ReadKey();
    }
}
```

The BenchmarkRunner object will evaluate the time spent on each and every method marked with the “[BenchMark]” attribute and produce report for these methods.

As you can see on the sample screen shot of a console report below.

```
C:\Users\cibou\OneDrive\Bureau\BenchmarkDotnet\Benchmarking\bin\Debug\net6.0\Benchmarking.exe
Arguments: --filter *

[Warning] ...
BenchmarkDotNet=v0.13.0.1165-ad6e4ec, OS=Windows 10.0.19044.2364 (21H2)
Intel Core i7-10750H CPU 2.60GHz, 1 CPU, 12 logical and 6 physical cores
.NET SDK=6.0.402
  [Host]     : .NET 6.0.8 (6.0.822.16304), X64 RyuJIT
  DefaultJob : .NET 6.0.8 (6.0.822.16304), X64 RyuJIT

| Method | Mean | Error | StdDev | Ratio | RatioSD | Gen 0 | Gen 1 | Gen 2 | Allocated |
|---|---|---|---|---|---|---|---|---|---|
| FindAllocatedInt32Box | 7.114 ns | 0.1433 ns | 0.1340 ns | 14.40 | 0.39 | 0.0119 | - | - | 40 B |
| FindAllocatedInt32BoxNoBox | 0.494 ns | 0.0022 ns | 0.0021 ns | 1.00 | 0.00 | - | - | - | - |

// * Hints *
Outliers  : BenchmarkDotNet.Benchmarks.FindAllocatedInt32Box.NoBox: Default -> 1 outlier was  removed (1.33 ns)
// * Legends *
  Mean   : Arithmetic mean of all measurements
  Error  : Half of 99.9% confidence interval
  StdDev : Standard deviation of all measurements
  Ratio  : Ratio of the time of the benchmark compared to the baseline
  RatioSD: Standard deviation of the ratio
  Gen 0  : GC Generation 0 collects per 1000 operations
  Gen 1  : GC Generation 1 collects per 1000 operations
  Gen 2  : GC Generation 2 collects per 1000 operations
  Allocated: Allocated memory per single operation (managed only, inclusive, 1KB = 1024B)
  1 ns   = 1 Nanosecond (0.000000001 sec)
```

In addition to the console report and the .html file BenchmarkRunner will also produce CSV file. That could be useful if you want to automate the following of the performances evolution (or build a dashboard around the results gathered).

You have also the possibility to archive the .html file report if you are refactoring for performances improvement and compare with the new version for headlining the effectiveness of the improvements done.

BenchmarkDotNet can also be added to the test project of your object, this way running the test provide the benchmarking and the validation of the test himself for your object at the same time (be careful in this case the report will be generate each time you run the test).
