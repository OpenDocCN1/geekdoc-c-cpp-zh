

以下 JavaScript 代码演示了如何访问所有之前的 WinRT 组件和功能。

```javascript
function () {
  // 在代码中让访问命名空间更加方便
  var winRTComps = Intel.WinRTComponents;

  // 注意：JavaScript 虚拟机通过驼峰命名法映射 WinRT API
  // 访问 WinRT 类型的静态方法和属性
  var s = winRTComps.staticMethod(null); // 注意：这里使用 JavaScript 的 "null"
  var struct = { index: 123, as: "Jeff", aenum: winRTComps.WinRTEnum.notnone };
  winRTComps.WinRTClass.staticProperty = struct;
  s = winRTComps.WinRTClass.staticProperty; // 读取回值

  // 如果方法有输出参数（out parameters），则它们将返回值
  // 并对象属性的形式返回
  var s = winRTComps.WinRTClass.outParameters();
  var name = s.value; // 返回值
  var struct = s.x; // 一个“输出”参数
  var year = s.year; // 另一个“输出”参数

  // 构造 WinRT 组件的实例
  var winRTClass = new winRTComps.WinRTClass(null);
  s = winRTClass.toString(); // 调用 ToString()

  // 演示 throw 和 catch
  try {
    winRTClass.throwingMethod();
  } catch (err) {
  }

  // 数组解析
  var a = [1, 2, 3, 4, 5];
  var sum = winRTClass.passArray(a);

  // 数组填充
  var arrayOut = [7, 7, 7]; // 注意：fillArray 看到的是全零！
  var length = winRTClass.fill(arrayOut); // 返回时，arrayOut = [0, 1, 2]

  // 数组返回
  a = winRTClass.returnArray(); // a = [1, 2, 3]

  // 传递集合并对其元素进行修改
  var localSettings = Windows.Storage.ApplicationData.current.localSettings;
  localSettings.values["Key1"] = "Value1";
  winRTClass.passAndModify(localSettings.values);
  // 返回时，localSettings.values 包含 2 个键值对

  // 调用重载方法
  winRTClass.someMethod(String); // 实际上调用 someMethod("")

  // 消费自动实现的事件
  var f = function (v) { return v.target };
  winRTClass.addEventListener("autoevent", f, false);
  s = winRTClass.raiseEvent(7);

  // 消费手动实现的事件
  winRTClass.addEventListener("manuellevent", f, false);
  s = winRTClass.raiseManualEvent(8);

  // 调用支持进度、取消和错误处理的异步方法
  var promise = winRTClass.doSomethingAsync();
  promise.then(
    function (result) { console.log("Async op complete: " + result); },
    function (error) { console.log("Async op error: " + error); },
    function (progress) {
      console.log("Async op progress: " + progress);
      //if (progress == 30) promise.cancel(); // 用于测试取消
    }
  );
}
```

# 多线程

- **第 26 章** 线程基础 .................................................................... . . . 669
- **第 27 章** 计算密集型异步操作. . . . . . 691
- **第 28 章** I/O 密集型异步操作 . . . . . . . 727
- **第 29 章** 原始线程同步构造结构. . . . . . 757
- **第 30 章** 混合线程同步构造结构 . . . . . . 789

# 第 26 章

# 线程基础

- 本章内容：
  - 为什么 Windows 支持线程？. . . . . . . . . . 669
  - 线程开销 . . . . . . . . . . . . . . . . . . . . 670
  - 停止这种疯狂行为. . . . . . . . . . . . . . . . . . . . . 674
  - CPU 趋势 . . . . . . . . . . . . . . . . . . . . . . . 677
  - CLR 线程与 Windows 线程 . . . . . . . . . . . . . 678
  - 使用专用线程执行异步计算密集型操作 . . . . . . . . . . . . . . . 678
  - 使用线程的原因. . . . . . . . . . . . . . . . . . . . . 681
  - 线程调度与优先级 . . . . . . . . . . . . . . . . 683
  - 前台线程 vs. 后台线程. . . . . . . . 688
  - 现在怎么办？. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 689

在本章中，我将介绍关于线程的基本概念，并为开发者提供一种概念化线程及其使用场景的方法。我将解释 Windows 为什么引入线程的概念、CPU 趋势，以及通用运行时（CLR）与线程之间的关系。

## 为什么 Windows 支持线程？

在本章中，我将介绍关于线程的基本概念，并为开发者提供一种概念化线程及其使用场景的方法。我将解释 Windows 为什么引入线程的概念、CPU 趋势，以及通用运行时（CLR）与线程之间的关系。

在 Windows 的早期阶段，每个应用程序只有一个线程。这意味着如果一个应用程序启动了长时间耗时的任务，整个操作系统就会冻结。这对用户来说是一个大问题，因为在任务运行期间他们无法使用其他应用程序。为了解决这个问题，微软引入了线程，允许应用程序同时执行多个任务。

## 线程开销

线程是非常棒的，因为它们让 Windows 在应用程序执行长时间耗时任务能够保持响应。此外，线程允许用户使用一个应用程序（如任务管理器）强制杀死一个由于执行长时间耗时任务而看起来假死的应用程序。但与每个虚拟化机制一样，线程都有相关的空间（内存消耗）和时间（运行时执行性能）开销。

