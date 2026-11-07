
- 2. 添加一个包含最后 **return** 语句的 main 函数

    ```cpp
    int main()
    {
        // Program code goes here.
        return 0;
    }
    ```

- 3. 在 main 函数中，插入一条语句，声明并初始化一个整型变量，并将该变量设为待匹配的值

    ```cpp
    int num = 3;
    ```

- 4. 接下来，插入一个 **switch** 语句以寻找匹配项

    ```cpp
    switch ( num )
    {
        case 1 : cout << num << ": Monday"; break ;
        case 2 : cout << num << ": Tuesday"; break ;
        case 3 : cout << num << ": Wednesday"; break ;
        case 4 : cout << num << ": Thursday"; break ;
        case 5 : cout << num << ": Friday"; break ;
    }
    ```

- 5. 在 **switch** 语句中，在最后一个 **case** 语句之后插入一个 **default** 语句

    ```cpp
    default : cout << num << ": Weekend day" ;
    ```

- 6. 保存、编译并运行程序以查看输出

- 7. 现在，编辑整型变量声明以更改其值，然后再次保存、编译并运行程序

    ```cpp
    int num = 6;
    ```

![](img/bf8dbdfb89042fadbaa73b4160c74bac_46_0.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_46_1.png)

请注意，**default** 语句后面不需要跟 **break** 关键字——因为 **default** 语句总是出现在 **switch** 语句的最后。

## for 循环

循环是程序中自动重复执行的一段代码。循环块中包含的所有语句完整执行一次称为一次“迭代”或“一轮”。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_47_0.png)

循环执行的迭代次数由循环内进行的条件测试控制。只要被测试的表达式保持为 **true**，循环就会继续——直到被测试的表达式变为 **false**，此时循环结束。

C++ 编程中的三种循环结构是 **for** 循环、**while** 循环和 **do-while** 循环。也许最常用的循环是 **for** 循环，其语法如下：

```
for ( initializer ; test-expression ; incrementer ) { statements }
```

初始化器为循环迭代次数计数器设置起始值。为此使用一个整型变量，传统上命名为“i”。

在循环的每次迭代中，都会对测试表达式求值，并且只有在该表达式为 **true** 时，该次迭代才会继续。当被测试的表达式变为 **false** 时，循环立即结束，不再执行语句。每次迭代时，计数器递增，然后执行语句。

循环可以嵌套在其他循环中——这样，内层循环会在外层循环的每次迭代中完整执行其所有迭代。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_47_1.png)

- 1. 通过指定要包含的 C++ 库类和要使用的命名空间前缀来开始一个新程序

    ```cpp
    #include <iostream>
    using namespace std ;
    ```

- 2. 添加一个包含最后 **return** 语句的 main 函数

    ```cpp
    int main()
    {
        // Program code goes here.
        return 0 ;
    }
    ```

- 3. 在 main 函数中，插入一条语句，声明一个用作循环迭代计数器的整型变量

    ```cpp
    int i ;
    ```

- 4. 接下来，插入一个 **for** 循环，在三次迭代的每一次中输出计数器值

    ```cpp
    for ( i = 1 ; i < 4 ; i++ )
    {
        cout << "Loop iteration: " << i << endl ;
    }
    ```

- 5. 保存、编译并运行程序以查看输出

![](img/bf8dbdfb89042fadbaa73b4160c74bac_48_0.png)

- 6. 现在，编辑变量声明以添加第二个计数器。

    ```cpp
    int i, j;        // Integer variable "j" added.
    ```

- 7. 在 for 循环块内，在输出语句之后添加一个内层循环，在每次迭代中输出其计数器值。

    ```cpp
    for (j = 1; j < 4; j++)
    {
        cout << "Inner loop iteration: " << j << endl;
    }
    ```

- 8. 再次保存、编译并运行程序，以查看内层循环在外层循环的每次迭代中完整执行。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_48_1.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_48_2.png)

另外，**for** 循环计数器可以通过使用 i-- 而不是 i++ 递增器来递减迭代，从而在每次迭代中倒计数。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_48_3.png)

在这些循环的第三次迭代中，递增器将计数器值增加到四——因此当下一次求值时，测试返回 false，循环结束。

## while 循环

上面介绍的 **for** 循环的替代方案使用 **while** 关键字，后面跟一个要求值的表达式。当表达式为 **true** 时，将执行测试表达式后面花括号内的语句。随后会再次对该表达式求值，**while** 循环将继续，直到发现该表达式为 **false**。

循环的语句块**必须**包含会影响被测试表达式的代码，以便将求值结果变为 **false**，否则会创建无限循环，从而锁定系统！当被测试表达式在第一次求值时就被发现为 **false** 时，**while** 循环的语句块将永远不会被执行。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_49_0.png)

如果不小心开始运行无限循环，请按 **Ctrl + C** 键终止进程。

**while** 循环的一个细微变体是将 **do** 关键字放在循环语句块之前，并在其后放置 **while** 测试，语法如下：

```
do { statements-to-be-executed } while ( test-expression ) ;
```

在 **do-while** 循环中，语句块将始终至少执行一次——因为表达式直到循环第一次迭代之后才会求值。

**break** 语句可以包含在任何类型的循环中，以便在满足测试条件时立即终止循环。**break** 确保不再执行该循环的后续迭代。

类似地，**continue** 语句可以包含在任何类型的循环中，以便在满足测试条件时立即终止该次特定迭代。**continue** 语句允许循环继续进行下一次迭代。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_49_1.png)

### while.cpp

- 1. 通过指定要包含的 C++ 库类和要使用的命名空间前缀来开始一个新程序

    ```cpp
    #include <vector>              // Include vector support.
    #include <iostream>
    using namespace std ;
    ```

- 2. 添加一个包含最后 **return** 语句的 main 函数

    ```cpp
    int main()
    {
        // Program code goes here.
        return 0 ;
    }
    ```

- 3. 在 main 函数中，插入语句来声明一个整型向量和一个整型变量循环计数器

    ```cpp
    vector <int> vec( 10 );
    int i = 0 ;
    ```

- 4. 接下来，插入一个 **while** 循环，在每次迭代中将计数器值赋给向量的一个元素

    ```cpp
    while ( i < vec.size() )
    {
        i++ ;                     // Increment the counter.
        vec[ i-1 ] = i ;                  // Assign count to element.
        cout << "|" << vec.at( i-1 ) ;
    }
    ```

- 5. 保存、编译并运行程序以查看输出

![](img/bf8dbdfb89042fadbaa73b4160c74bac_50_0.png)

- 6. 编辑 **while** 循环，在递增器之后立即添加一个 **continue** 语句，使循环跳过其第三次迭代

    ```cpp
    if ( i == 3 ) { cout << " | Skipped" ; continue ; }
    ```

- 7. 在 **continue** 语句之后，现在添加一个 **break** 语句，使循环在其第八次迭代时退出

    ```cpp
    if ( i == 8 ) { cout << endl << "Done" ; break ; }
    ```

- 8. 再次保存、编译并运行程序，以查看循环现在省略了一些迭代

![](img/bf8dbdfb89042fadbaa73b4160c74bac_50_1.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_50_2.png)

在此示例中，必须使用预处理指令包含 vector 库。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_50_3.png)

**break** 和 **continue** 语句的位置很重要——它们必须出现在递增器之后，以避免创建无限循环，但要出现在影响程序的其他语句之前，以避免执行那些语句。
