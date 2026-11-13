

## ask_and_move 函数的规格说明

```cpp
void ask_and_move(binary_tree_node<string>*& current_ptr);
// Precondition: current_ptr points to a nonleaf node in a binary taxonomy
// tree.
// Postcondition: The question at the current node has been asked. The
// current pointer has been shifted left (if the user answered yes) or right
// (for a no answer).
```

play 使用的第二个重要函数叫做 learn。learn 函数在游戏到达叶节点且叶节点上的动物猜错时使用。该函数从用户处获取信息，从而改进树，具体规范如下：

## learn 函数的规格说明

```cpp
void learn(binary_tree_node<string>* Leaf_ptr);
// Precondition: leaf_ptr is a pointer to a leaf in a taxonomy tree.
// This leaf contains a wrong guess that was just made.
// Postcondition: Information has been elicited from the user,
// and the tree has been improved.
```

使用这两个函数，play 的实现相对简短，如下所示：

```cpp
void play(binary_tree_node<string>* current_ptr)
// Precondition: current_ptr points to the root of a binary taxonomy tree
// with at least two leaves.
// Postcondition: One round of the animal game has been played,
// and maybe the tree has been improved.
{
    cout << "Think of an animal, then press the return key.";
    eat_line();
    while (!current_ptr->is_leaf())
        ask_and_move(current_ptr);
    cout << ("My guess is " + current_ptr->data() + ". ");
    if (inquire("Am I right?"))
        learn(current_ptr);
    else
        cout << "I knew it all along!" << endl;
}
```

在此实现中，我们使用 inquire 函数来提问“我猜对了吗？”。还使用了一个名为 eat_line 的函数，用于读取并丢弃直到下一个换行符之前的所有字符。这两个函数都是我们实用函数工具包的一部分（参见附录 I）。那么还剩下什么要做呢？实现 ask_and_move 和 learn 两个函数，我们现在就来做。

## ask_and_move 函数。

此函数有一个参数，即指向分类树中某个节点的当前指针。该函数询问该节点处的问题，并根据用户的回答将当前指针向下移动到子树。使用 useful.h 中的 inquire 函数，其实现非常简短：

```cpp
void ask_and_move(binary_tree_node<string>*& current_ptr)
{
    cout << current_ptr->data( );
    if (inquire(" Please answer:"))
        current_ptr = current_ptr->left( );
    else
        current_ptr = current_ptr->right( );
}
```

## learn 函数。

当游戏到达叶节点并做出错误猜测时，会调用此函数。该函数采取多个步骤来改进分类树。该函数的参数是指向包含错误猜测的节点的指针，如下原型所示：

```cpp
void learn(binary_tree_node<string>* leaf_ptr);
```

例如，假设我们刚刚从这棵树中错误地猜中了一只袋鼠：

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_522_0.png)

learn 函数首先设置三个局部字符串变量：

- 1. 猜中了什么动物？这来自 current_ptr->data()，并存储在名为 guess_animal 的局部变量中。在本示例中，guess_animal 是“袋鼠”。
- 2. 正确的动物是什么？用户对此问题的回答被读入名为 correct_animal 的局部字符串变量。为读取答案，我们使用字符串的 getline 函数。该函数读取一整行输入（包括空格），并将该行放入字符串中。在本示例中，假设用户的回答是“浣熊”。
- 3. 什么是能区分正确动物与被猜动物的是/否问题？在我们的示例中，我们需要一个能区分袋鼠和浣熊的问题。用户可能会提供问题“你是有袋类动物吗？”，我们将把这个问题存储在另一个名为 new_question 的局部字符串变量中。

设置好这三个字符串后，我们还需要一条信息。具体来说，我们需要知道新动物对用户刚刚提供的问题回答是是还是否。在我们的示例中，我们需要知道浣熊对“你是有袋类动物吗？”这个问题的回答是是还是否。当然，浣熊不是有袋类动物，因此基于这个否定回答，我们可以按以下步骤进行：

- 1. 将新问题复制到 current_ptr 的数据字段中。
- 2. 将被猜的动物复制到一个新叶节点，该节点被创建为当前节点的左子节点。
- 3. 将正确的新动物复制到一个新叶节点，该节点被创建为当前节点的右子节点。

在我们的示例中，这些步骤如下所示改进了分类树：

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_523_0.png)

另一种可能性是，新动物对新问题回答是。例如，用于区分浣熊和袋鼠的问题可能是“你有环纹尾巴吗？”在这种情况下，新动物（浣熊）将作为新问题的左子节点添加，旧动物（袋鼠）添加到右侧。

learn 函数的实现是图 10.9 中完整的动物猜谜程序的一部分。

## 动物猜谜程序——改进

我们的动物程序存在一个问题：每次执行程序时，它最初只知道四种动物。一项改进将允许它将当前的分类树存储在文件中，并在每次程序启动时读取该文件。这样，程序就能记住它学过的所有动物。

## 图 10.9 动物猜谜程序

### 一个程序

```cpp
// FILE: animal.cxx
// This animal guessing program illustrates the use of the binary tree node class.

#include <cstdlib>    // Provides EXIT_SUCCESS
#include <iostream>   // Provides cout
#include <string>     // Provides string class
#include "bintree.h"  // Provides the binary tree node class
#include "useful.h"  // Provides eat_line, inquire (from Appendix I)
using namespace std;
using namespace main_savitch_10;  // binary_tree_node

// PROTOTYPES for functions used by this game program:
void ask_and_move(binary_tree_node<string>* &current_ptr);
// Precondition: current_ptr points to a nonleaf node in a binary taxonomy tree.
// Postcondition: The question at the current node has been asked. The current pointer has
// been shifted left (if the user answered yes) or right (for a no answer).

binary_tree_node<string>* beginning_tree( );
// Postcondition: The return value is the root pointer of a new small taxonomy tree.

void instruct( );
// Postcondition: Instructions for playing the game have been printed to the screen.

void learn(binary_tree_node<string>* leaf_ptr);
// Precondition: leaf_ptr is a pointer to a leaf in a taxonomy tree. The leaf contains a wrong
// guess that was just made.
// Postcondition: Information has been elicited from the user, and the tree has been improved.

void play(binary_tree_node<string>* current_ptr);
// Precondition: current_ptr points to the root of a binary taxonomy tree with at least two leaves.
// Postcondition: One round of the animal game has been played, and maybe the tree has
// been improved.

int main( )
{
    binary_tree_node<string> *taxonomy_root_ptr;

    instruct( );
    taxonomy_root_ptr = beginning_tree( );
    do
        play(taxonomy_root_ptr);
    while (inquire("Shall we play again"));
    cout << "Thank you for teaching me a thing or two." << endl;

    return EXIT_SUCCESS;
}
```

## （图 10.9 续）

```cpp
void ask_and_move(binary_tree_node<string>*& current_ptr)
// Library facilities used: bintree.h, string, useful.h
{
    cout << current_ptr->data( );
    if (inquire( "Please answer: "))
        current_ptr = current_ptr->left( );
    else
        current_ptr = current_ptr->right( );
}
```

```cpp
binary_tree_node<string>* beginning_tree( )
// Library facilities used: bintree.h, string
{
    binary_tree_node<string> *root_ptr;
    binary_tree_node<string> *child_ptr;

    const string root_question("Are you a mammal?");
    const string left_question("Are you bigger than a cat?");
    const string right_question("Do you live underwater?");
    const string animal1("Kangaroo");
    const string animal2("Mouse");
    const string animal3("Trout");
    const string animal4("Robin");

    // Create the root node with the question "Are you a mammal?"
    root_ptr = new binary_tree_node<string>( root_question );

    // Create and attach the left subtree.
    child_ptr = new binary_tree_node<string>( left_question );
    child_ptr->set_left( new binary_tree_node<string>( animal1 ) );
    child_ptr->set_right( new binary_tree_node<string>( animal2 ) );
    root_ptr->set_left(child_ptr);

    // Create and attach the right subtree.
    child_ptr = new binary_tree_node<string>( right_question );
    child_ptr->set_left( new binary_tree_node<string>( animal3 ) );
    child_ptr->set_right( new binary_tree_node<string>( animal4 ) );
    root_ptr->set_right(child_ptr);

    return root_ptr;
}
```

```cpp
void instruct( )
// The implementation of this function is omitted—write it yourself!
```

