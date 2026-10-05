
[content]

## 6.5. 迭代示例

```cpp
cout << "*";
count++;
}
// // 将光标移动到下一行
cout << endl;
// 到下一行
row++;
}
```

当用户运行列表 6.20 (startree.cpp) 并输入 7 时，程序将显示：

![](img/e326304bd50fbc4f7d5a64c1487eb635_147_0.png)

列表 6.20 (startree.cpp) 使用了嵌套在 `while` 循环中的顺序 `while` 循环。外部 `while` 循环负责在每次执行循环体时绘制树的一行：

- 当用户输入大于零的值时，程序将执行外层循环体；如果用户输入零或更小的值，程序将终止且什么都不做。这是预期的行为。

- 外层 `while` 循环体中的最后一个语句 `row++;` 确保了行数每次循环时都会增加 1；因此，它最终将等于高度（因为进入循环时它最初小于高度），循环将终止。不存在无限循环的可能性。

- 外层循环体包含多条语句；因此，循环体必须被括在大括号内。当一组语句被括在大括号内时，就形成了一个块（block）。变量的作用域（声明变量并可以使用它的源代码部分）是从它的声明点到其声明所在块的结束。例如，变量 `height` 和 `row` 声明在 `main` 体的块中；因此，外层 `while` 语句的体是 `main`；因此，`count` 是在外层 `while` 语句中声明的。尝试在外层 `while` 语句之外使用 `count` 将导致错误。

变量 `x` 对于特定代码段是局部意味着什么？`x` 在其作用域之外不存在。程序中可能存在其他名为 `x` 的变量，但它们是不同的变量。在同一个程序中拥有两个同名的变量似乎很奇怪，但想一下同一个房间里可以有两个同名的人。他们是不同的人，但名字相同。同样，变量的含义取决于它的上下文，它的名称并不一定是唯一的。

两个内层循环起着不同的作用：

- 第一个内层循环打印空格。打印的空格数量等于外层循环第一次执行时树的高度，并在每次迭代中都会减少。这是正确的行为，因为随后的每一行包含更少的空格但更多的星号。
- 第二个内层循环打印构成树的星号行。在外层循环第一次执行时，该次数为 0，因此不打印左侧星号；会打印一个中间星号（树的顶部），且不打印右侧星号。循环每次执行，左侧和右侧星号的数量增加一个，并打印同一个中间星号；因此，树每向下移动每一行都会变宽。观察 `2*row + 1` 的值如何完美地表达所需的星号数量。
- 看起来是不对称的，不需要第三个内层循环在打印星号之后打印行尾空格。这些空格是不可见的，所以没有理由打印它们！

### 6.5.2 打印质数

质数是一个大于1的整数，它的因子（也称为除数）只有1和它本身。例如，29 是质数（只有 1 和 29 能整除它而无余数），但 28 不是（2、4 和 14 是它的因子）。质数曾是数学家的智力好奇，但现在它们在密码学和计算机安全中起着重要作用。

任务是编写一个程序，显示到用户输入的值为止的所有质数。列表 6.21 (printprimes.cpp) 提供了一个解决方案。

> 列表 6.21: printprimes.cpp

```cpp
#include <iostream>

using namespace std;

int main() {
	int max_value;
	cout << "显示到什么值之前的质数? ";
	cin >> max_value;
	int value = 2; // 最小质数
	while (value <= max_value) {
		// 检查 value 是否为质数
		// bool prime = true; // 暂时假设 prime 是质数
		// 尝试从 2 到 value - 1 的所有可能的因子
		int trial_factor = 2;
		bool is_prime = true;
		while (trial_factor < value) {
			if (value % trial_factor == 0) {
				is_prime = false; // 找到了因子
				break;
			}
			// 无需继续；它不是质数
			trial_factor++;
		}
		if (is_prime) {
			cout << value << " "; // 显示质数
		}
		value++; // 尝试下一个潜在质数
	}
	cout << endl; // 将光标移动到下一行
}
```

列表 6.21 (printprimes.cpp) 在输入 90 时产生输出：

```
显示到什么值之前的质数? 90
2 3 5 7 11 13 17 19 23 29 31 37 41 43 47 53 59 61 67 71 73 79 89
```

6.21 (print_primes.cpp) 的逻辑比之前的稍微复杂一点。对于 `while` 循环引入了新的变量：`trial_factor` 和 `is_prime`，它们是外层 `while` 语句的（startree.cpp）。`trial_factor` 初始化为 2，`is_prime` 初始化为 `true`，意味着 `value` 是质数：

```cpp
int trial_factor = 2;
while (trial_factor < value) {
    if (value % trial_factor == 0) {
        is_prime = false; // 找到了因子
        break; // 无需继续；它不是质数
    }
    trial_factor++;
}
```

当 `value % trial_factor == 0` 时，`is_prime` 变为 `false`——正当 `trial_factor` 整除 `value`。如果 `is_prime` 变为 `false`，循环无法继续，如果不是，循环将结束：

```cpp
if (is_prime) {
    cout << value << " "; // 显示质数
}
```

一些重要的问题：

- 1. 如果用户输入 2，它是质数吗？在这种情况下 `max_value = 2`，所以 `while` 条件

```cpp
value <= max_value
```

不成立。

- 2. 如果用户输入小于 2 的数字，会有打印内容吗？`while` 确保了小于 2 的值不被考虑。`while` 体永远不会进入。只打印换行符。这种行为是正确的。

- 3. 内层循环保证终止吗？为了进入内层循环，`trial_factor` 必须小于 `value`。`value` 在循环中没有变化，但 `trial_factor` 因此在每次迭代中都会增加。最终，`trial_factor` 等于 `value`，循环终止。

- 4. 外层循环保证终止吗？为了进入外层循环体，`value` 必须小于或等于 `max_value`，`max_value` 在循环中没有变化；它在外层循环体的最后一个语句中增加，而在其他地方没有修改。由于内层循环正如前面保证终止，最终 `value` 将超过 `max_value`，循环将结束。

我们重新排列了内层的逻辑，以使用 `break` 语句。当前版本是：

```cpp
while (trial_factor < value) {
    if (value % trial_factor == 0) {
        is_prime = false; // 找到了因子
        break; // 无需继续；它不是质数
    }
    trial_factor++;
}
```

我们可以重写为：

```cpp
while (is_prime == (value % trial_factor != 0)) {
    trial_factor++; // 尝试下一个因子
}
```

这个不带 `break` 的版本引入了一个稍微复杂的 `while` 条件，但将 `if` 语句移动到了循环体内部。`is_prime` 在循环之前被初始化为 `true`。每次循环重启时，如果任何 `value % trial_factor` 为零，`is_prime` 就会变为 `false`。这正当 `trial_factor` 是 `value` 的因子时。如果 `is_prime` 变为 `false`，循环无法继续，如果它从不变为 `false`，则在 `trial_factor` 等于 `value` 时循环结束。由于运算符的优先级，括号并不是必要的。但为了提高可读性，因为包含 `==` 和 `!=` 的表达式对人类解析来说很别扭。当在
