
# 1247 奇数复习题答案

+ 37. A) 30
B) 30
C) 0
D) 0
E) 20
F) 10
G) 10
H) 20

## 第 11 章

+ 1. `static`
3. `static`
5. `friend`
7. 成员赋值 (Memberwise assignment)
9. `this`
11. 后置递增（或递）
13. 包含 (has-a)

+ 15. 拷贝构造函数
`overloaded operator`
`overloaded operator`
`copy constructor`

17. 将 `static` 关键字放在函数的原型中。函数的调用通过作用域运算符将函数名连接到*类*名来实现。

19. 在对象组合中，一个对象嵌套在另一个对象内部，这创建了“包含”关系。当一个类是另一个类的友元时，不存在嵌套。如果类 A 是类 B 的友元，A 的成员函数可以访问 B 的所有成员，包括私有成员。

21. 如果使用指针成员引用动态分配的内存，成员赋值将只拷贝指针的内容，而不是指针引用的内存区域。这意味着将存在两个指向内存中相同地址的对象。如果其中一个对象操作了该内存区域，更改将对两个对象都生效。此外，如果其中一个对象释放了内存，该内存对两个对象来说都不再包含有效信息。

23. 如果对象按值传递给拷贝构造函数，那么在传递给拷贝构造函数之前必须创建参数的拷贝。但这样创建拷贝本身又需要调用拷贝构造函数并按值传递原始参数。这个过程将无限持续。

```cpp
25. Dollars Dollars::operator++; // 前置

Dollars Dollars::operator++(int); // 后置
```

## 附录 D 奇数复习题答案

+ 27. `ostream &operator<< (ostream &strm, Length obj);`

+ 29. 重载提供了一种更直观的对象操作方式，类似于处理原始数据类型的方式。

+ 31. 成员 (members)

+ 33. 宠物 (Pet)

+ 35. 私有 (private)

+ 37. 不可访问 (inaccessible), 私有 (private), 私有 (private)

+ 39. 不可访问 (inaccessible), 保护 (protected), 公开 (public)

+ 41. 最后 (last)

+ 43. A) 类声明的第一行应当为：
`class Car : public Vehicle`
此外，类声明应以分号结束。

+ B) 类声明的第一行应当为：
`class Truck : public Vehicle`

## 第 12 章

+ 1. C 字符串 (C-string)
3. 字符串字面量 (string literal)
5. 空终止符 (null terminator)
7. `ostringstream`
9. 拼接 (concatenate)

+ 11. `strcpy`
13. `strcmp`
15. `atoi`

+ 19. `char lastChar(const char *str) {`
  // 移动到末尾的空终止符
  `while (*str != 0)`
    `str++;`
  // 回退到最后一个字符
    `str--;`
  `return *str;`
`}`

+ 21. `h`
23. `9`

+ 25. 大多数编译器会打印“not equal”。某些编译器只存储每个字面量字符串的拷贝；这些编译器会打印“equal”，因为所有“a”的拷贝将存储在相同的地址。

+ 27. 磨损 (abrasion)

29. A) 这可能是一个逻辑错误，因为 C 字符串不应使用 `==` 运算符进行比较

B) `atoi` 将字符串转换为整数，而不是将整数转换为字符串。

C) 编译器不会在 `string1` 中分配足够的空间来容纳两个字符串。

D) `strcmp` 比较的是 C 字符串而不是字符。

## 第 13 章

+ 1. 文件名 (file name)

+ 3. 关闭 (close)

+ 5. `ifstream`, `ofstream`, `fstream`

+ 7. `ifstream`

+ 9. `ofstream people("people.dat");`

+ 11. `fstream places("places.dat");`

+ 13. `pets.open("pets.dat", ios::in);`
`fstream pets("pets.dat", ios::in);`

+ 15. 空 (null) 或 `0`

+ 17. `cout`

+ 19. `getline`

+ 21. `put`

+ 23. 文本 (text), ASCII 文本 (ASCII text)

+ 25. 结构 (structures)

+ 27. 读取 (read)

+ 29. 顺序的 (sequential)

+ 31. `seekg`

+ 33. `tellg`

+ 35. `ios::beg`

+ 37. `ios::cur`

39. 以二进制模式打开文件，跳转到末尾，然后使用 `tellg` 确定最后一个字节的位置：

```cpp
ifstream inFile(fileName, ios::binary);

inFile.seekg(0, ios::end);

long len = inFile.tellg();
```

41. 以二进制模式打开两个文件，第一个文件用于输入，第二个用于输出。跳转到第一个文件的末尾，并在写入第二个文件的同时在第一个文件中不断回退。

```cpp
fstream inFile(fileName, ios::in | ios::binary);

fstream outFile(fileName2, ios::out | ios::binary);
```

```cpp
char ch;

// seek位到源文件末尾

// 然后定位到最后一个字符 之前的位置

infile.seekg(0, ios::end);

infile.seekg(-1, ios::cur);

while (true) {

    // 我们正定位在最后一个字符 
    // 之前

    infile.seekg(0, ios::end);

    infile.seekg(-1, ios::cur);

    // ...

}
```

# 第 1253 奇数复习题答案

B) 指针最终会变为 NULL，此时访问 `p->next` 将导致错误。将 while 循环中的 `p->next` 替换为 `p`。此外，该函数未声明 `void` 返回类型。

C) 函数应该声明返回类型为 `void`。该函数在尝试移动到列表的下一个节点时，错误地使用了 `p++` 而不是 `p = p->next`。

D) 将 `nodeptr->next = NULL;` 替换为 `delete nodeptr;`

# 第 18 章

- 1. 先入队列 (First In Out)
3. 静态栈在创建时一次性分配所有存储。通常，静态栈使用数组实现，而栈使用链表。

- 5. 它获取现有的容器并在其之上实现新接口，以适应不同的用途。

- 7. 先进先出 (First In First Out)
9. 队列头部

- 11. 列表 (lists) 和双队列 (deques)

| 栈顶 (Top of Stack) |
| :--- |
| 19 |
| 栈底 (Bottom of Stack) 数组缓冲区：

15. 假设是一个循环数组缓冲区：

| 10 | 9 | 12 |
| :--- | :--- | :--- |
| 尾 (rear) | 头 (front) | |

17. 使用两个栈，一个主栈和一个辅助栈。主栈存储当前封装的所有元素。

- 要入队新元素，将其推入主栈。
- 要出队元素，继续从主栈弹出元素并将其推入辅助栈，直到主栈为空，然后从辅助栈中取出元素并存储到变量 X 中。继续从辅助栈弹出元素并推回主栈，直到栈为空。返回存储的元素 X。
- 要检查队列是否为空，查看主栈是否为空。

# 第 19 章

- 1. 根节点 (root node)
3. 叶子节点 (leaf node)

5. 中序、前序和后序

```cpp
7. struct TreeNode {
    int value;
    TreeNode *left, *middle, *right;
};
```

```cpp
9. 要按前序遍历三叉树，访问根节点，然后遍历左子树和右子树。

preorder(ternarytree)
If (ternarytree != NULL)
    visit the root
    preorder left subtree of ternarytree
    preorder middle subtree of ternarytree
    preorder right subtree of ternarytree
End If
End preorder
```

11. 我们必须决定是在遍历完左树后立即访问根节点，还是在遍历中间子树后访问。

```cpp
13. largest(TreeNode *tree)
Set a pointer * p to the root node of tree
While node at p has a right child Do
    Set p to the right child of the node at p
End While
return value in the node at p
End largest
```

```cpp
15. smallest(TreeNode *tree)
Set a pointer * p to the root node of tree
While node at p has a left child Do
    Set p to the left child of the node at p
End While
return value in the node at p
End smallest
```
