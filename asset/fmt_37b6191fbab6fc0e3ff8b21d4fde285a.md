
再次注意，我们讨论的“类型”是指表示特定内建类型类型的 C 结构。对象的类是完全不同的一个概念。内置类的类存储在名为 `rb_cClassName`（例如 `rb_Object`）的 C 全局变量中；模块被命名为 `rb_Modulname`。

不建议直接修改这些 C 结构中的数据——你可能想这样做，但请不要碰触。通常你会使用提供的 C 函数来操作 Ruby 数据（我们稍后会详细讨论这一点）。

出于效率考虑，你可能需要深入这些结构以获取数据。为了解引用这些结构的成员，你必须将通用的 `VALUE` 强制转换为相应的结构类型。ruby 有许多宏可以为你执行强制转换，这些宏是 `RCLASSNAME`（返回结构）和 `RCLASSNAME_XXX` 后者允许你访问结构中的特定字段。例如，`STRING(obj)` 将返回指向 `obj` 的 `RString` 结构的引用；`STRING_PTR(obj)` 和 `STRING_LEN(obj)` 返回内容和长度。对于哈希 (`RHASH`)、文件 (`RFILE`) 等，也有类似的访问器。完整列表见第 29.2 页和 841 页。

## 1.9 之前的字符串访问

在 Ruby 1.8.6 之前，你会直接访问 `RSTRING` 字段来获取长度字符串数据指针。那么，如何编写一个能同时兼容这两种技术的扩展呢？也许像这样：

```
# if defined(RSTRING_LEN)
#   define RSTRING_LEN(x) (RSTRING(x)->len)
#   define RSTRING_PTR(x) (RSTRING(x)->ptr)
# endif
```

## 全局变量

大多数时候，你的扩展会实现类，而 Ruby 代码会使用这些类。你在 Ruby 代码和 C 代码之间共享的数据将整齐地封装在类对象内部。这应该是它的做法。

有时，你可能需要实现一个全局变量，以便你的 C 扩展和 Ruby 代码都能访问。

实现此点的最简单方法是拥有一个变量 `VALUE`（即一个 Ruby 对象）。然后你将此 C 变量的地址绑定到 Ruby 变量名。在这种情况下，`$` 前缀是可选的，但它有助于明确这是一个全局变量。确保你不要使用基于栈的变量：一旦帧消失，它将不再存在。

```
static VALUE hardware_list;
static VALUE Init_SysInfo() {
  rb_define_class(...);
  hardware_list = rb_ary_new();
  rb_define_variable("Hardware", &hardware_list);
  rb_ary_push(hardware_list, rb_str_new("DVD3"));
  rb_ary_push(hardware_list, rb_str_new("CDPLAYER1"));
  rb_ary_push(hardware_list, rb_str_new("CDPLAYER2"));
}
```

Ruby 随后可以作为 `$hardware` 访问 C 变量 `hardware_list`：

`$hardware => ["DVD3", "CDPLAYER1", "CDPLAYER2"]`

有时，情况更复杂。如果你想定义一个在访问时必须计算其值的全局变量，你可以通过使用钩子变量（hooked variables）和虚拟变量来实现。钩子变量是一个真实的变量，当访问相应的 Ruby 变量时，由一个命名函数进行初始化。虚拟变量类似，但它们从不存储；其值完全取决于钩子的评估。详情请参见第 868 页开始的 API 章节。

## 表 29.2. 对象访问器宏

| | | |

|---|---|---|

| RClass c; | | |

| RCLASS_TBL(c) | 指向方法的指针 | |

| RCLASS_SUPER(c) | 指向父类的指针 | |

| RModule m; | | |

| RMODULE_IV_TBL(m) | | |

| RMODULE_SUPER(m) | | |

| RFloat v; | | |

| STRING_VALUE(v) | | |

| STRING_LEN(str) | | |

| STRING_PTR(str) | | |

| STRING_END(str) | | |

| RArray a; | | |

| RARRAY_LEN(a) | | |

| RARRAY_PTR(a) | | |

| RARRAY_SIZE(a) | | |

| RHash h; | | |

| RHASH_TBL(h) | | |

| RHASH_ITER(h) | | |

| RHASH_NONE(h) | | |

| RHASH_SIZE(h) | | |

| RFile f; | | |

| RFILE_LEN(f) | | |

| RFILE_PTR(f) | | |

| RCLASS_NAME(c) | 返回类名 | |

| RCLASS_NAME_P(c) | | |

| RCLASS_SIZ(c) | | |

| RCLASS_ID(c) | | |

| RCLASS_OBJ(c) | | |

| RCLASS_TRUE(c) | | |

| RCLASS_EMPTY(c) | | |

| RCLASS_ANY(c) | | |

| RCLASS_MOD(c) | | |

| RCLASS_DATA(c) | | |

| RCLASS_TYPE(c) | | |

| RCLASS_INT(c) | | |

| RCLASS_STR(c) | | |

| RCLASS_FLOAT(c) | | |

| RCLASS_HASH(c) | | |

| RCLASS_REG(c) | | |

| RCLASS_SYM(c) | | |

| RCLASS_TRUE(c) | | |

| RCLASS_FALSE(c) | | |

| RCLASS_NIL(c) | | |

| RCLASS_DATA(c) | | |

在独立的线程中运行。例如，一个线程可能会调用你的扩展库来启动某些长时间运行的操作，如文件复制。你的代码使用 `rb_tbr` 允许解释器的其余部分在此过程中继续运行。但可能其他线程之一调用了 `exit` 来关闭解释器。Ruby 需要与你线程中正在进行的任何操作协调这种关闭行为。它通过调用你传递给 `rb_tbr` 的取消阻塞函数来实现这一点。该函数负责终止任何由 `rb_tbr` 启动的操作。

让我们来看一些使用此特性的 C 代码。这个示例取自主解释器中的 `bignum.c`，但它适用于扩展中的代码。

首先，代码定义了一个结构，用于将参数传递给并行执行的函数。在这个例子，同一个结构也被传递给了取消阻塞函数：

```
struct big_mul_struct {
    VALUE x, y, z, stop;
};
```

这里是用于乘两个大整数（bignums）的方法体。我们删掉了中间一些无聊的内容。

```
static VALUE
rb_big_mul10(VALUE x, VALUE y)
{
    struct big_mul_struct bms;
    volatile VALUE z;
    /* .../
    bms.x = x;
    bms.y = y;
    bms.stop = QFalse;
    if (RBIGNUM_LEN(x) + RBIGNUM_LEN(y) > 10000) {
        z = rb_thread_blocking_region(bignum, &bms, rb_big_stop, &bms.stop);
    }
    else {
        z = bignum(&bms);
    }
    return z;
}
```

对你重要的代码位于方法的末尾。如果相乘的数字很大，它会调用 `rb_thread_blocking_region`，传递要运行的函数 (`bignum1`)、传递给它的参数 (`bms`)以及取消阻塞函数和参数 (`rb_big_stop` 和 `bms`)。如果数字低于阈值，它会直接调用 `bignum1`。

现在让我们来看取消阻塞函数 `rb_big_stop`：

```
static void
rb_big_stop(void *ptr)
{
    VALUE *stop = (VALUE)ptr;
    *stop = Qtrue;
}
```

如果被调用，它简单地将其参数所引的位置设置为 `Qtrue`。

那么它是如何提前停止计算的？让我们来看 `bigmul1`（再次省略了部分细节）：

```
static VALUE
bigmul1(void*ptr)
{
    struct big_mul_struct *bms = (struct big_mul_struct*)ptr;
    long i, j;
    VALUE x = bms->x, y = bms->y, z = bms->z;
    /* ... */
    for (i = 0; i < RBIGNUM_LEN(x); i++) {
        if (bms->stop) return nil;
        /* ...
        * 执行下一位 ... */
    }
    return z;
}
```

因此，如果取消阻塞函数被调用，它会将结构体的 `stop` 成员设置为 `Qtrue`。然后，在循环中执行乘法时（该循环在独立线程中运行）会注意到标志位已被设置并提前退出，返回 `nil`。

## 线程、进程与 I/O

如果你传递给 `rb_iter` 的代码执行了 I/O 或与外部进程同步，那么在编写取消阻塞函数时，你将面临一个艰难的决定。中断 I/O 是复杂的，且很可能取决于系统。幸运的是，Ruby 为你提供了一个“大锤”来解决这个特定的坚果。如果你将第三个参数传递 `RUBY_UBF_IO` 或 `RUBY_UBF_PROCESS`（第四个参数为 `NULL`），Ruby 将使用一个默认函数，直接杀死执行处理的线程。以下是读取文件描述符的解释器方法代码：

```
static int
rb_read_internal(int fd, void *buf, size_t count)
{
    struct io_internal_struct iis;
    iis.fd = fd;
    iis.buf = buf;
    iis.cap = count;
    return rb_thread_blocking_region(count, &iis, RUBY_UBF_IO, 0);
}
```

你需要决定是否在你的扩展中使用这些内置函数。例如，在更新数据库时，你可能希望通过简单地终止线程来执行受控的关闭。

## 扩展

现在我们涵盖了足够的基础知识，可以回到我们的示例——与 Ruby 接口，并在两个世界之间共享数据和行为。

## 封装结构

我们有了一个控制音频单元的库，并准备好将其接入 Ruby。厂商的头文件看起来如下所示：

```c
typedef struct _cdukebox {
    int status;
    int request;
    void *data;
    char pending;
    int unit_id;
    void *stats;
} CDJukebox;

// 分配一个新的播放机
CDJukebox *new_jukebox(void);

// 将播放机分配给播放器
void assign_jukebox(CDJukebox *jb, int unit_id);

// 释放（并下线）
void free_jukebox(CDJukebox *jb);

// 磁寻磁盘、跟踪并通知进度
void jukebox_seek(CDJukebox *jb, int track);

// ...

// 报告统计
double get_stats(CDJukebox *jb);
```

我们有一个控制音频单元的库，并准备好将其接入 Ruby。厂商的头文件看起来如下：

```c
typedef struct _cdukebox {
    int status;
    int request;
    void *data;
    char pending;
    int unit_id;
    void *stats;
} CDJukebox;

// 分配一个新的播放机
CDJukebox *new_jukebox(void);

// 将播放机分配给播放器
void assign_jukebox(CDJukebox *jb, int unit_id);

// 释放（并下线）
void free_jukebox(CDJukebox *jb);

// 磁寻磁盘、跟踪并通知进度
void jukebox_seek(CDJukebox *jb, int track);

// ...

// 报告统计
double get_stats(CDJukebox *jb);
```

我们有了一个控制音频单元的库，并准备好将其接入 Ruby。这个结构代表了播放机的状态，因此是封装的良好的候选对象。这个 C 类型在 Ruby 实例变量中是分离的。当垃圾回收器回收它时，你如何处理它？如果你需要释放某些资源（关闭文件、清理锁），等等。

Ruby 使用“标记-清除”垃圾回收机制。在标记阶段，Ruby 寻找指针并将其标记为“正在使用”（如果这些区域本身包含指针，它们引用的内存也会被标记，等等）。在标记阶段结束时，所有被引用的内存都被标记，而孤立对象没有。随后开始清除，释放未标记的内存。

为了参与 Ruby 的标记-清除垃圾回收过程，你必须定义你的结构，并可能标记从你的结构到其他结构的引用。这两个函数都在垃圾回收器的标记阶段调用。如果你的结构引用其他 Ruby 对象，你的标记函数需要使用 `rb_gc_mark` 来识别这些对象。如果结构没有引用其他 Ruby 对象，你可以简单地传递 0 作为函数指针。

当对象被处理时，垃圾回收器将调用释放函数来释放它。如果你自己分配了任何内存（例如使用 `Data_Make_Struct`），你需要传递一个释放函数——即使是标准 C 库的释放函数。对于你分配的复杂结构，你的释放函数可能需要遍历结构以释放所有分配的内存。

让我们来看数字播放器接口。厂商库通过它的各个函数通过 `CDJukebox` 结构传递信息。这个结构代表了播放机的状态，因此是封装的良好的候选对象。你通过调用 CDPlayer 方法创建新实例。然后你想将创建的结构封装在新的 CDPlayer 对象中。执行此操作的代码片段如下：（我们稍后会讨论那个类参数。）

```
CDJukebox *jukebox;
VALUE obj;
// 厂商库创建播放机
jukebox = new_jukebox();
// 然后我们将其封装在 CDPlayer 对象中
obj = Data_Wrap_Struct(klass, 0, jukebox);
```

## 分配函数

分配函数负责创建你的对象所使用的内存。如果你实现的对象除了 Ruby 实例变量外没有使用任何其他数据，那么你就不需要编写分配函数——Ruby 的默认分配器就能正常工作。但如果你的类封装了一个 C 结构体，你将需要在分配函数中为该结构体分配空间。分配函数会传递被分配对象的类。在我们的案例中，它可能是 `cdPlayer`，但我们将使用给定的参数，因为这意味着在被子类化时我们的工作能够正常进行：

```c
static VALUE cd_alloc(VALUE class) {
CDJukebox *jukebox;
VALUE obj;
// Veldor 库创建 Jukebox
jukebox = new_jukebox();
// 我们将其封装在 Ruby CDPlayer 对象内部
obj = Data_wrap_Struct(class, 0, cd_free, jukebox);
return obj;
}
```

然后，你需要在类的初始化代码中注册你的分配函数：

```c
void init_CDPlayer() {
cdPlayer = rb_define_class("CDPlayer", rb_cobject);
rb_define_alloc_func(CDPlayer, cd_alloc);
// ...
}
```

大多数对象还需要定义一个初始化器。分配函数创建一个空的、未初始化的对象，我们需要填充特定的值。在 CD 播放器的情况下，构造函数被调用时传入了与该对象关联的单元（unit）：

```c
static VALUE cd_initialize(VALUE self, VALUE unit) {
int unit_id;
CDJukebox *jukebox;
Data_Get_Struct(self, CDJukebox, jukebox);
unit_id = NUM2INT(unit);
assign_jukebox(jukebox, unit_id);
return self;
}
```

这种多步对象创建协议的原因之一是，它允许解释器处理通过“后门手段”创建对象的情况。一个例子是对象从其序列化格式反序列化时。在这里，解释器会创建一个空对象（通过调用分配器），但它无法调用初始化器（因为它不知道要使用哪些参数）。另一个常见情况是对象被复制（duplicate）或克隆（clone）。

这里隐藏着另一个问题。由于用户可以跳过构造函数，你需要确保你的分配代码让返回的对象处于有效状态。它可能不包含由 `#initialize` 设置时本应的所有信息，但它至少需要是用的。

## 克隆对象

所有的 Ruby 对象都可以通过 `dup` 和 `clone` 两个方法进行复制。这两个方法非常相似。它们都通过调用分配函数产生接收者类的新实例，然后从原始对象中复制任何实例变量。`clone` 更进一步，它会复制原始对象的单例类（如果有的话）和标志（例如指示对象已冻结的标志）。你可以将 `dup` 理解为内容的拷贝，而将 `clone` 理解为完整对象的拷贝。
