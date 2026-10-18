

{
    if (turnover <= THRESHOLD)
        return ( cost + (LOW_MARKUP * cost) );
    else
        return ( cost + (HIGH_MARKUP * cost) );
}

完整的程序如显示5.9所示。

## 显示5.9 超市定价（第1部分，共2部分）

```
1 //Determines the retail price of an item according to
2 //the pricing policies of the Quick-Shop supermarket chain.
3 #include <iostream>
4 const double LOW_MARKUP = 0.05; //5%
5 const double HIGH_MARKUP = 0.10; //10%
6 const int THRESHOLD = 7;//Use HIGH_MARKUP if not expected
7 //to sell in 7 days or less.
8 void introduction();
9 //Postcondition: Description of program is written on the screen.
10 void getInput(double& cost, int& turnover);
11 //Precondition: User is ready to enter values correctly.
12 //Postcondition: The value of cost has been set to the
13 //wholesale cost of one item. The value of turnover has been
14 //set to the expected number of days until the item is sold.
15 double price(double cost, int turnover);
16 //Precondition: cost is the wholesale cost of one item.
17 //turnover is the expected number of days until sale of the item.
18 //Returns the retail price of the item.
19 void giveOutput(double cost, int turnover, double price);
20 //Precondition: cost is the wholesale cost of one item; turnover is the
21 //expected time until sale of the item; price is the retail price of the item.
22 //Postcondition: The values of cost, turnover, and price have been
23 //written to the screen.
24 int main()
25 {
26     double wholesaleCost, retailPrice;
27     int shelfTime;
28     introduction();
29     getInput(wholesaleCost, shelfTime);
30     retailPrice = price(wholesaleCost, shelfTime);
31     giveOutput(wholesaleCost, shelfTime, retailPrice);
32     return 0;
33 }
34     //Uses iostream:
35 void introduction()
```

## 程序测试

测试程序的一个重要技术是测试所有种类的输入。对于“种类”的输入，我们并没有精确的定义，但在实践中，通常很容易判断一个程序处理哪些种类的输入数据。就我们的超市程序而言，主要有两种输入：使用5%低加价率的输入和使用10%高加价率的输入。因此，我们应该至少测试一种商品预期在货架上存放少于7天的情况，以及至少一种预期存放超过7天的情况。

另一种测试策略是测试边界值。不幸的是，边界值是又一个模糊的概念。如果某个输入（测试）值是程序行为发生改变的值，那么它就是边界值。例如，在我们的超市程序中，程序行为在预期上架天数为7天时发生变化。因此，7是一个边界值；程序对于小于或等于7的天数的行为不同于大于7的天数。因此，我们应该至少测试一种商品预期在货架上恰好存放7天的情况。通常，你还应该测试与边界值相差一步的输入，因为你在确定边界时很容易出现正负1的偏差。因此，我们应该用预期在货架上存放6天、7天和8天的商品输入来测试程序。（这除了前一段描述的测试输入外，那些输入应远低于7天和远高于7天。）

## 自测练习

- 13. 函数定义可以出现在另一个函数定义的内部吗？
- 
- 14. 函数定义可以包含对另一个函数的调用吗？
- 
- 15. 用前置条件和后置条件重写显示5.8中order函数的函数声明注释。
- 
- 16. 为预定义函数`sqrt`给出一个前置条件和一个后置条件，该函数返回其参数的平方根。

## 5.4 测试与调试函数

> “我看到了那个可怜虫——我所创造的悲惨怪物。”
> 
> 玛丽·沃斯通克拉夫特·雪莱，*《弗兰肯斯坦》*

## 桩和驱动程序

每个函数都应作为与程序其他部分分离的独立单元来设计、编码和测试。这是自顶向下设计策略的精髓。当你把每个函数当作一个独立单元时，你就把一个庞大的任务转化为一系列更小、更易于管理的任务。但是，如何在函数所属的程序之外测试它呢？你编写一个专门的程序来进行测试。例如，显示5.10显示了一个用于测试函数getInput的程序，该函数在显示5.9的程序中使用过。

## 显示5.10 驱动程序（第1部分，共2部分）

```
1   //Driver program for the function getInput.
2   #include <iostream>
3
4   void getInput(double& cost, int& turnover);
5   //Precondition: User is ready to enter values correctly.
6   //Postcondition: The value of cost has been set to the
7   //wholesale cost of one item. The value of turnover has been
8   //set to the expected number of days until the item is sold.
9
10  int main()
11  {
12      using namespace std;
13      double wholesaleCost;
14      int shelfTime;
15      char ans;
16
17      cout.setf(ios::fixed);
18      cout.setf(ios::showpoint);
19      cout.precision(2);
20      do
21      {
22          getInput(wholesaleCost, shelfTime);
23
24          cout << "Wholesale cost is now $"
25             << wholesaleCost << endl;
26          cout << "Days until sold is now "
27             << shelfTime << endl;
28
29          cout << "Test again?"
30             << " (Type y for yes or n for no): ";
31          cin >> ans;
32          cout << endl;
33      } while (ans == 'y' || ans == 'Y');
34
35      return 0;
36  }
```

## 显示5.10 驱动程序（第2部分，共2部分）

```
37  //Uses iostream:
38  void getInput(double& cost, int& turnover)
39  {
40      using namespace std;
41      cout << "Enter the wholesale cost of item: $";
42      cin >> cost;
43      cout << "Enter the expected number of days until sold: ";
44      cin >> turnover;
45  }
```

## 示例对话

```
Enter the wholesale cost of item: $123.45
Enter the expected number of days until sold: 67
Wholesale cost is now $123.45
Days until sold is now 67
Test again? (Type y for yes or n for no): y

Enter the wholesale cost of item: $9.05
Enter the expected number of days until sold: 3
Wholesale cost is now $9.05
Days until sold is now 3
Test again? (Type y for yes or n for no): n
```

像这样的程序称为驱动程序。这些驱动程序是临时工具，可以非常简单。它们不需要花哨的输入例程。它们不需要执行最终程序将执行的所有计算。它们所要做的只是尽可能简单地获得合理的函数参数值——通常来自用户——然后执行函数并显示结果。如显示5.10中程序所示的循环，允许你在不必重新运行程序的情况下，用不同的参数重新测试该函数。

如果你分别测试每个函数，你会发现在程序中的大部分错误。而且，你会找出哪些函数包含错误。如果你只测试整个程序，你可能会发现是否存在错误，但可能不知道错误在哪里。更糟糕的是，你可能以为你知道错误在哪里，但实际上却错了。

一旦你完整地测试了一个函数，你就可以在用于其他函数的驱动程序中使用它。每个函数都应该在一个程序中测试，并且它是该程序中唯一未测试的函数。但是，在测试其他函数时，使用一个已经完整测试过的函数是可以的。如果发现错误，你就知道错误在未测试的函数中。例如，在使用显示5.10中的驱动程序完整测试了函数getInput之后，你可以将getInput作为输入例程用于驱动程序中，以测试其余函数。

