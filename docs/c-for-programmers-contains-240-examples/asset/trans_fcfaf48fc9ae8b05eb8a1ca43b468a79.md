

在本节中，你使用调试器的 **step** 和 **finish** 命令来调试程序执行期间调用的函数。你看到了 **next** 命令如何跳过函数调用。你还了解到 **quit** 命令会结束一次调试会话。

## H.5 watch 命令

*watch command* 告诉调试器监视一个数据成员。当该数据成员即将改变时，调试器会通知你。在本节中，你将使用 watch 命令来查看 Account 对象的 data member balance 在执行期间如何被修改。

- **1. 启动调试器。** 通过输入 `gdb FigH_03` 启动调试器。

- **2. 设置断点并运行程序。** 输入 `break 14` 在第 14 行设置断点。然后，使用命令 `run` 运行程序。调试器和程序将在第 14 行的断点处暂停（图 H.26）。

```text
(gdb) break 14
Breakpoint 1 at 0x80486e5: file FigH_03.cpp, line 14.
(gdb) run
Starting program: /home/nuke/AppH/FigH_03

Breakpoint 1, main () at FigH_03.cpp:14
14        Account account1( 50 ); // create Account object
(gdb)
```

**Fig. H.26** | 运行程序直到第一个断点。

- **3. 监视类的 data member。** 通过输入 `watch account1.balance` 在 account1 的 balance 数据成员上设置监视（图 H.27）。此监视被标记为 watchpoint 2，因为 watchpoints 使用与 breakpoints 相同的序号进行标记。你可以对当前作用域中的任何变量或对象的 data member 设置监视。每当被监视变量的值发生变化时，调试器就会进入中断模式并通知你该值已发生变化。

```text
(gdb) watch account1.balance
Hardware watchpoint 2: account1.balance
(gdb)
```

**Fig. H.27** | 在数据成员上设置监视点。

- **4. 执行构造函数。** 使用 `next` 命令执行构造函数并初始化 account1 对象的 balance 数据成员。调试器指示 balance 数据成员的值已更改，显示旧值和新值，并在第 20 行进入中断模式（图 H.28）。

```text
(gdb) next
Hardware watchpoint 2: account1.balance

Old value = 0
New value = 50
Account (this=0xbfcd6b90, initialBalance=50) at Account.cpp:20
20        if ( initialBalance < 0 )
(gdb)
```

**Fig. H.28** | 进入构造函数。

- **5. 退出构造函数。** 输入 `finish` 以完成构造函数的执行并返回到 `main`。

- **6. 从账户中取款。** 输入 `continue` 继续执行并在提示处输入取款金额。程序正常执行。图 H.3 的第 25 行调用 Account 成员函数 debit 以按指定金额减少 Account 对象的 balance。图 H.2 的第 34 行在函数 debit 内部更改 balance 的值。调试器会通知你此更改并进入中断模式（图 H.29）。

```text
(gdb) continue
Continuing.
account1 balance: $50

Enter withdrawal amount for account1: 13

attempting to subtract 13 from account1 balance

Hardware watchpoint 2: account1.balance

Old value = 50
New value = 37
0x0804893b in Account::debit (this=0xbfcd6b90, amount=13) at Account.cpp:34
34            balance = balance - amount;
(gdb)
```

**Fig. H.29** | 当变量被更改时进入中断模式。

- **7. 继续执行。** 输入 continue——程序将完成执行函数 main，因为程序不会再尝试对 balance 进行任何额外更改。调试器会移除对 account1 的 balance 数据成员的监视，因为当函数 main 结束时，account1 对象超出作用域。移除 watchpoint 会导致调试器进入中断模式。再次输入 continue 以完成程序的执行（图 H.30）。

```text
(gdb) continue
Continuing.
account1 balance: $37

Watchpoint 2 deleted because the program has left the block in which its expression is valid.
0xb7da0595 in exit () from /lib/tls/i686/cmov/libc.so.6
(gdb) continue
Continuing.

Program exited normally.
(gdb)
```

**Fig. H.30** | 继续到程序结束。

- **8. 重新启动调试器并重置变量的监视。** 输入 run 重新启动调试器。再次通过输入 watch account1.balance 在 account1 数据成员 balance 上设置监视。此 watchpoint 被标记为 watchpoint 3。输入 continue 继续执行（图 H.31）。

```text
(gdb) run
Starting program: /home/nuke/AppH/FigH_03

Breakpoint 1, main () at FigH_03.cpp:14
14          Account account1( 50 ); // create Account object
(gdb) watch account1.balance
Hardware watchpoint 3: account1.balance
(gdb) continue
Continuing.
Hardware watchpoint 3: account1.balance

Old value = 0
New value = 50
Account (this=0xbfd8eb90, initialBalance=50) at Account.cpp:20
20          if ( initialBalance < 0 )
(gdb)
```

**Fig. H.31** | 重置对数据成员的监视。

- **9. 移除对数据成员的监视。** 假设你只想在程序执行的某一部分监视一个数据成员。你可以通过输入 delete 3 移除调试器对变量 balance 的监视（图 H.32）。输入 continue——程序将完成执行而不会再次进入中断模式。

```text
(gdb) delete 3
(gdb) continue
Continuing.
account1 balance: $50

Enter withdrawal amount for account1: 13

attempting to subtract 13 from account1 balance

account1 balance: $37

Program exited normally.
(gdb)
```

**Fig. H.32** | 移除监视。

在本节中，你使用 watch 命令使调试器在变量值更改时通知你。你使用 delete 命令在程序结束前移除对数据成员的监视。

## H.6 总结

在本附录中，你学习了如何在调试器中插入和移除断点。断点允许你在程序执行时暂停，以便使用调试器的 print 命令检查变量值，这有助于你定位和修复逻辑错误。你使用 print 命令检查表达式的值，并使用 set 命令更改变量的值。你还学习了调试器命令（包括 step、finish 和 next 命令），可用于确定函数是否正确执行。你学习了如何使用 watch 命令在数据成员的作用域内跟踪数据成员。最后，你学习了如何使用 info break 命令列出为程序设置的所有断点和监视点，以及使用 delete 命令移除单个断点和监视点。

## 参考书目

如需了解更多 C++ 书籍、文章等，请访问 Deitel C++ 资源中心

www.deitel.com/cplusplus

- Abrahams, D. and A. Gurtovoy. *C++ Template Metaprogramming: Concepts, Tools, and Techniques from Boost and Beyond.* Boston, MA: Addison-Wesley Professional, 2004.
- Alexandrescu, A. *Modern C++ Design: Generic Programming and Design Patterns Applied.* Boston, MA: Addison-Wesley Professional, 2001.
- Alhir, S. *UML in a Nutshell.* Cambridge, MA: O’Reilly & Associates, Inc., 1998.
- Almarode, J. “Object Security.” *Smalltalk Report* Vol. 5, No. 3 November/December 1995, 15–17.
- *American National Standard, Programming Language C++.* (ANSI Document ISO/IEC 14882), New York, NY: American National Standards Institute, 1998.
- Anderson, A. E. and W. J. Heinze. *C++ Programming and Fundamental Concepts.* Englewood Cliffs, NJ: Prentice Hall, 1992.
- Arciniegas, F. *C++ XML.* Indianapolis, IN: Sams, 2001.
- Arlow, J. and I. Neustadt. *UML 2 and the Unified Process: Practical Object-Oriented Analysis and Design, Second Edition.* Boston, MA: Addison-Wesley Professional, 2005.
- Astle, D. and K. Hawkins. *Beginning OpenGL Game Programming.* Boston, MA: Course Technology PTR, 2004.
- Bar-David, T. *Object-Oriented Design for C++.* Englewood Cliffs, NJ: Prentice Hall, 1993.
- Beck, K. “Birds, Bees, and Browsers—Obvious Sources of Objects.” *The Smalltalk Report* Vol. 3, No. 8, June 1994, 13.
- Becker, P. “Shrinking the Big Switch Statement.” *Windows Tech Journal* Vol. 2, No. 5, May 1993, 26–33.
- Becker, P. “Conversion Confusion.” *C++ Report* October 1993, 26–28.
- Berard, E. V. *Essays on Object-Oriented Software Engineering: Volume I.* Englewood Cliffs, NJ: Prentice Hall, 1993.
- Binder, R. V. “State-Based Testing.” *Object Magazine* Vol. 5, No. 4, August 1995, 75–78.
- Binder, R. V. “State-Based Testing: Sneak Paths and Conditional Transitions.” *Object Magazine* Vol. 5, No. 6, October 1995, 87–89.
- Blum, A. *Neural Networks in C++: An Object-Oriented Framework for Building Connectionist Systems.* New York, NY: John Wiley & Sons, 1992.
- Booch, G. *Object Solutions: Managing the Object-Oriented Project.* Reading, MA: Addison-Wesley, 1996.
- Booch, G. *Object-Oriented Analysis and Design with Applications, Third Edition.* Reading, MA: Addison-Wesley, 2005.

