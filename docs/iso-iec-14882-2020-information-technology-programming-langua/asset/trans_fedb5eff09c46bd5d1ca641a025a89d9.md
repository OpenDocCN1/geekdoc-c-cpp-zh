

## 17.12.5.2.3 Promise 访问 [coroutine.handle.noop.promise]

```
noop_coroutine_promise& promise() const noexcept;
```

返回：与此协程句柄关联的 promise 对象的引用。

## 17.12.5.2.4 地址 [coroutine.handle.noop.address]

```
constexpr void* address() const noexcept;
```

返回：ptr。

说明：noop_coroutine_handle 的 ptr 始终为非空指针值。

## 17.12.5.3 函数 noop_coroutine [coroutine.noop.coroutine]

```
noop_coroutine_handle noop_coroutine() noexcept;
```

返回：指向一个协程的句柄，该协程在恢复或销毁时没有可观察到的效果。

说明：从 noop_coroutine 返回的句柄可能与从另一次 noop_coroutine 调用返回的句柄相等，也可能不相等。

## 17.12.6 轻量级 awaitables [coroutine.trivial.awaitables]

```
namespace std {
  struct suspend_never {
    constexpr bool await_ready() const noexcept { return true; }
    constexpr void await_suspend(coroutine_handle<>) const noexcept {}
    constexpr void await_resume() const noexcept {}
  };
  struct suspend_always {
    constexpr bool await_ready() const noexcept { return false; }
    constexpr void await_suspend(coroutine_handle<>) const noexcept {}
    constexpr void await_resume() const noexcept {}
  };
}
```

[说明 1：类型 suspend_never 和 suspend_always 可用于指示 await 表达式要么永不挂起，要么始终挂起，并且在任一情况下都不产生值。——说明结束]

## 17.13 其他运行时支持 [support.runtime]

## 17.13.1 通用 [support.runtime.general]

头文件 <csetjmp>（非局部跳转）、<csignal>（信号处理）、<cstdarg>（可变参数）和 <cstdlib>（运行时环境 getenv，system）提供了与 C 代码的进一步兼容性。

对函数 getenv（17.2.2）的调用，只要环境未被修改，就不会引入数据竞争（16.4.6.10）。

[说明 1：对 POSIX 函数 setenv 和 putenv 的调用会修改环境。——说明结束]

对 setlocale 函数（28.5）的调用可能会与对 setlocale 函数的其他调用或受当前 C 区域设置影响的函数调用引入数据竞争。实现应表现得好像除了 locale::global 之外的任何库函数都不会调用 setlocale 函数。

## 17.13.2 头文件 <cstdarg> 概要 [cstdarg.syn]

```
namespace std {
  using va_list = see below;
}
```

```
#define va_arg(V, P) see below
#define va_copy(VDST, VSRC) see below
#define va_end(V) see below
#define va_start(V, P) see below
```

头文件 <cstdarg> 的内容与 C 标准库头文件 <stdarg.h> 相同，但有以下更改：ISO C 对头文件 <stdarg.h> 中 va_start 宏的第二个参数施加的限制在本文件中有所不同。参数 parmN 是函数定义的可变参数列表中的最右参数（... 之前的那个）。221 如果参数 parmN 是包展开（13.7.4）或由 lambda 捕获（7.5.5）产生的实体，则程序格式错误，无需诊断。如果参数 parmN 是引用类型，或是与传递参数时没有对应参数的类型不兼容的类型，则行为未定义。

另见：ISO C 7.16.1.1

## 17.13.3 头文件 <csetjmp> 概要 [csetjmp.syn]

```
namespace std {
  using jmp_buf = see below;
  [[noreturn]] void longjmp(jmp_buf env, int val);
}

#define setjmp(env) see below
```

1 头文件 <csetjmp> 的内容与 C 标准库头文件 <setjmp.h> 相同。

2 函数签名 longjmp(jmp_buf jbuf, int val) 在本文件中的行为受到更严格的限制。setjmp/longjmp 调用对如果用 catch 和 throw 替换 setjmp 和 longjmp 会导致具有自动存储期的任何对象的非平凡析构函数被调用，则行为未定义。对 setjmp 或 longjmp 的调用如果在协程（7.6.2.4）的挂起上下文中被调用，则行为未定义。

另见：ISO C 7.13

## 17.13.4 头文件 <csignal> 概要 [csignal.syn]

```
namespace std {
  using sig_atomic_t = see below;

  // 17.13.5, signal handlers
  extern "C" using signal-handler = void(int); // exposition only
  signal-handler* signal(int sig, signal-handler* func);

  int raise(int sig);
}

#define SIG_DFL see below
#define SIG_ERR see below
#define SIG_IGN see below
#define SIGABRT see below
#define SIGFPE see below
#define SIGILL see below
#define SIGINT see below
#define SIGSEGV see below
#define SIGTERM see below
```

1 头文件 <csignal> 的内容与 C 标准库头文件 <signal.h> 相同。

## 17.13.5 信号处理程序 [support.signal]

1 对 signal 函数的调用与由此安装的信号处理程序的任何后续调用同步。

2 一个普通的无锁原子操作是对第 31 条款中的函数 f 的调用，使得：

+   （2.1）—— f 是函数 atomic_is_lock_free()，或
+   （2.2）—— f 是成员函数 is_lock_free()，或
+   （2.3）—— f 是在对象 A 上调用的非静态成员函数，使得 A.is_lock_free() 返回 true，或
+   （2.4）—— f 是非成员函数，并且对于传递给 f 的每个指向原子的指针参数 A，atomic_is_lock_free(A) 返回 true。

3 除非评估包含以下之一，否则评估是信号安全的：

+   （3.1）—— 对任何标准库函数的调用，除了普通的无锁原子操作和明确标识为信号安全的函数之外；

> [说明 1：这隐式排除了使用依赖于库提供的内存分配器的 `new` 和 `delete` 表达式。——说明结束]

+   （3.2）—— 对具有线程存储期的对象的访问；
+   （3.3）—— `dynamic_cast` 表达式；
+   （3.4）—— 抛出异常；
+   （3.5）—— 控制进入 *try-block* 或 *function-try-block*；
+   （3.6）—— 初始化需要动态初始化的具有静态存储期的变量（6.9.3.3，8.8）²²²；或
+   （3.7）—— 等待具有静态存储期的变量的初始化完成（8.8）。

如果信号处理程序调用包含非信号安全的评估，则行为未定义。

4 如果 signal 函数在第一个参数等于导致处理程序调用的信号的信号编号的情况下被调用，则该函数是信号安全的。

另见：ISO C 7.14

## Assessment 2: Instructions

本评估包含 3 个问题。请回答所有问题。

+   1. 问题 1（20 分）：人工智能基础的简答题。
+   2. 问题 2（30 分）：搜索算法的解题任务。
+   3. 问题 3（50 分）：人工智能伦理的案例研究。

> > 说明：这是一项个人评估。不允许合作。

| 问题 | 分数 | 主题 |
| --- | --- | --- |
| Q1 | 20 | 人工智能基础 |
| Q2 | 30 | 搜索算法 |
| Q3 | 50 | 人工智能伦理 |

将您的答案作为 PDF 文件提交。确保每页都出现您的姓名和学号。

```
```
请将文件命名为：ASSESS2_<YourID>.pdf
```
```

截止日期：星期日，11:59 PM（AEST）。逾期提交将受到处罚。

```
// 18.6, object concepts
template<class T>
    concept movable = see below;
template<class T>
    concept copyable = see below;
template<class T>
    concept semiregular = see below;
template<class T>
    concept regular = see below;

// 18.7, callable concepts
// 18.7.2, concept invocable
template<class F, class... Args>
    concept invocable = see below;

// 18.7.3, concept regular_invocable
template<class F, class... Args>
    concept regular_invocable = see below;

// 18.7.4, concept predicate
template<class F, class... Args>
    concept predicate = see below;

// 18.7.5, concept relation
template<class R, class T, class U>
    concept relation = see below;

// 18.7.6, concept equivalence_relation
template<class R, class T, class U>
    concept equivalence_relation = see below;

// 18.7.7, concept strict_weak_order
template<class R, class T, class U>
    concept strict_weak_order = see below;
}
```

## 18.4 语言相关概念 [concepts.lang]

## 18.4.1 通用 [concepts.lang.general]

第 18.4 条款包含与语言特性相对应的概念的定义。这些概念表达了类型、类型分类和基本类型属性之间的关系。

## 18.4.2 概念 same_as [concept.same]

```
template<class T, class U>
    concept same-as-impl = is_same_v<T, U>;        // exposition only

template<class T, class U>
    concept same_as = same-as-impl<T, U> && same-as-impl<U, T>;
```

[说明 1：same_as<T, U> 包含 same_as<U, T>，反之亦然。——说明结束]

## 18.4.3 概念 derived_from [concept.derived]

```
template<class Derived, class Base>
    concept derived_from =
        is_base_of_v<Base, Derived> &&
        is_convertible_v<const volatile Derived*, const volatile Base*>;
```

[说明 1：derived_from<Derived, Base> 当且仅当 Derived 公共且无歧义地派生自 Base，或 Derived 和 Base 是忽略 cv-限定符的同一类类型时得到满足。——说明结束]

