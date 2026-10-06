

## 图 14-17 蜜蜂和蝗虫是昆虫的特化版本

![](img/c939132f78787c7f339c6977b3fc8c85_574_0.png)

除了常见的昆虫特征外，蜜蜂还有自己独特的特征，例如蜇刺的能力。

除了常见的昆虫特征外，蝗虫也有自己独特的特征，例如跳跃的能力。

所有昆虫都具有某些特征。

## 继承与“是一个”（Is a）关系

当一个对象是另一个对象的特化版本时，它们之间存在一种“是一个……”的的关系。例如，蝗虫是一只昆虫。以下是几个“是一个……”的关系的例子：

- * 贵宾是一只狗。
- 汽车是一辆交通工具。
- 花朵是一株植物。
- 矩形是一个形状。
- 足球运动员是一名运动员。

当对象之间存在“是一个……”的的关系时，意味着特化对象具有泛化对象的所有特征，再加上使其变得特殊的额外特征。在面向对象编程中，继承被用于在类之间创建“是一个……”的关系。你可以通过创建另一个该类的特化版本类来扩展该类的功能。

继承涉及一个父类和一个子类。父类是泛化类，子类是特化类。你可以将子类类为父类的扩展版本。子类从父类继承字段和方法，而无需重写其中任何一个。此外，可以向子类中添加新的字段和方法，这使得它成为父类的特化版本。

> 注意：父类也称为基类（base classes），子类也称为派生类（derived classes）。这两组术语都是正确的。为了一致起见，本文将使用父类（superclass）和子类（subclass）术语。

让我们来看一个如何继承的示例。大多数老师会给学生布置各种评分活动。评分活动可以给出一个数值分数，如 70、85、90 等，以及一个字母等级，如 A、B、C、D 或 F。

图 14-18 显示了 GradedActivity 类的 UML 图，该类设计用于存储评分活动的数值分数。setScore 方法设置数值分数，getScore 方法返回数值分数。getgrade 方法返回与数值分数相对应的字母。类列表 14-8 显示了该类的伪代码。程序 14-4 中的伪代码演示了该类如何工作。

## 图 14-18 GradedActivity 类的 UML 图

| GradedActivity |
| :--- |
| - score : Real |
| + setScore(s : Real) |
| + getScore() : Real |
| + getGrade() : String |

## 类列表 14-8

```
1 Class GradedActivity
2 // score 字段存储一个数值分数。
3 Private Real score
4
5 // 变异器 (Mutator)
6 Public Module setScore(Real s)
7 Set score = s
8 End Module
9
10 // 访问器 (Accessor)
11 Public Function getScore()
12 Return score
13 End Function
14
15 // getgrade 方法
16 Public Function getGrade()
17 // 用于存储等级的局部变量。
18 Declare String grade
19
20 // 确定等级。
21 If score >= 90 Then
22 Set grade = "A"
23 Else If score >= 80 Then
24 Set grade = "B"
25 Else If score >= 60 Then
26 Set grade = "C"
27 Else
28 Set grade = "D"
29 End If
30 // 返回等级。
31 Return the grade.
32 Return grade
33 End Function
34 End Class
```

## 程序 14-4

```
1 Module main()
2 // 用于存储测试分数的变量。
3 Declare Real testScore
4
5 // 用于引用
aded GradedActivity 对象的变量。
7 Declare GradedActivity test
8
9 // 创建一个 GradedActivity 对象。
10 Set test = New GradedActivity()
11
12 // 从用户处获取测试分数。
13 Display "Enter a numeric test score."
14 Input testScore
15
16 // 将分数存储在对象中。
17 test.setScore(testScore)
18
19 // 显示对象的等级。
20 Display "The grade for that test is " + 
21 test.getGrade()
22 End Module
```

## 程序输出（输入部分加粗显示）

Enter a numeric test score.
**89 [Enter]**The grade for that test is B

## 程序输出（输入部分加粗显示）

Enter a numeric test score.
**75 [Enter]**The grade for that test is C

蜜蜂和蝗虫是昆虫的特化版本

除了常见的昆虫特征外，蜜蜂还有自己独特的特征，例如蜇刺的能力。除了常见的昆虫特征外，蝗虫也有自己独特的特征，例如跳跃的能力。

所有昆虫都具有某些特征。

## 继承与“是一个”的关系

当一个对象是另一个对象的特化版本时，它们之间存在一种“是一个……”的关系。例如，蝗虫是一只昆虫。以下是几个“是一个……”的关系例子：

- * 贵宾是一只狗。
- 汽车是一辆交通工具。
- 花朵是一株植物。
- 矩形是一个形状。
- 足球运动员是一名运动员。

当对象之间存在“是一个……”的关系时，意味着特化对象具有泛化对象的所有特征，再加上使其变得特殊的额外特征。在面向对象编程中，继承被用于在类之间创建“是一个……”的关系。你可以通过创建另一个该类的特化版本类来扩展该类的功能。

继承涉及一个父类和一个子类。父类是泛化类，子类是特化类。你可以将子类类为父类的扩展版本。子类从父类继承字段和方法，而无需重写其中任何一个。此外，可以向子类中添加新的字段和方法，这使得它成为父类的特化版本。

> 注意：父类也称为基类（base classes），子类也称为派生类（derived classes）。这两组术语都是正确的。为了一致起见，本文将使用父类（superclass）和子类（subclass）术语。

让我们来看一个如何继承的示例。大多数老师会给学生布置各种评分活动。评分活动可以给出一个数值分数，如 70、85、90 等，以及一个字母等级，如 A、B、C、D 或 F。

图 14-18 显示了 GradedActivity 类的 UML 图，该类设计用于存储评分活动的数值分数。setScore 方法设置数值分数，getScore 方法返回数值分数。getgrade 方法返回与数值分数相对应的字母。类列表 14-8 显示了该类的伪代码。程序 14-4 中的伪代码演示了该类如何工作。

## 图 14-18 GradedActivity 类的 UML 图

| GradedActivity |
| :--- |
| - score : Real |
| + setScore(s : Real) |
| + getScore() : Real |
| + getGrade() : String |

## 类列表 14-8

```
1 Class GradedActivity
2 // score 字段存储一个数值分数。
3 Private Real score
4
5 // 变异器 (Mutator)
6 Public Module setScore(Real s)
7 Set score = s
8 End Module
9
10 // 访问器 (Accessor)
11 Public Function getScore()
12 Return score
13 End Function
14
15 // getgrade 方法
16 Public Function getGrade()
17 // 用于存储等级的局部变量。
18 Declare String grade
19
20 // 确定等级。
21 If score >= 90 Then
22 Set grade = "A"
23 Else If score >= 80 Then
24 Set grade = "B"
25 Else If score >= 60 Then
26 Set grade = "C"
27 Else
28 Set grade = "D"
29 End If
30 // 返回等级。
31 Return the grade.
32 Return grade
33 End Function
34 End Class
```

## 程序 14-4

```
1 Module main()
2 // 用于存储测试分数的变量。
3 Declare Real testScore
4
5 // 用于引用
6 GradedActivity 对象的变量。
7 Declare GradedActivity test
8
9 // 创建一个 GradedActivity 对象。
10 Set test = New GradedActivity()
11
12 // 从用户处获取测试分数。
13 Display "Enter a numeric test score."
14 Input testScore
15
16 // 将分数存储在对象中。
17 test.setScore(testScore)
18
19 // 显示对象的等级。
20 Display "The grade for that test is " + 
21 test.getGrade()
22 End Module
```

## 程序输出（输入部分加粗显示）

Enter a numeric test score.
**89 [Enter]**The grade for that test is B

## 程序输出（输入部分加粗显示）

Enter a numeric test score.
**75 [Enter]**The grade for that test is C

蜜蜂和蝗虫是昆虫的特化版本

除了常见的昆虫特征外，蜜蜂还有自己独特的特征，例如蜇刺的能力。除了常见的昆虫特征外，蝗虫也有自己独特的特征，例如跳跃的能力。

所有昆虫都具有某些特征。

## 继承与“是一个”的关系

当一个对象是另一个对象的特化版本时，它们之间存在一种“是一个……”的关系。例如，蝗虫是一只昆虫。以下是几个“是一个……”的关系例子：

- * 贵宾是一只狗。
- 汽车是一辆交通工具。
- 花朵是一株植物。
- 矩形是一个形状。
- 足球运动员是一名运动员。

当对象之间存在“是一个……”的关系时，意味着特化对象具有泛化对象的所有特征，再加上使其变得特殊的额外特征。在面向对象编程中，继承被用于在类之间创建“是一个……”的关系。你可以通过创建另一个该类的特化版本类来扩展该类的功能。

继承涉及一个父类和一个子类。父类是泛化类，子类是特化类。你可以将子类类为父类的扩展版本。子类从父类继承字段和方法，而无需重写其中任何一个。此外，可以向子类中添加新的字段和方法，这使得它成为父类的特化版本。

> 注意：父类也称为基类（base classes），子类也称为派生类（derived classes）。这两组术语都是正确的。为了一致起见，本文将使用父类（superclass）和子类（subclass）术语。

让我们来看一个如何继承的示例。大多数老师会给学生布置各种评分活动。评分活动可以给出一个数值分数，如 70、85、90 等，以及一个字母等级，如 A、B、C、D 或 F。

图 14-18 显示了 GradedActivity 类的 UML 图，该类设计用于存储存储活动的数值分数。setScore 方法设置数值分数，getScore 方法返回数值分数。getgrade 方法返回与数值分数相对应的字母。类列表 14-8 显示了该类的伪代码。程序 14-4 中的伪代码演示了该类如何工作。

## 图 14-18 GradedActivity 类的 UML 图

| GradedActivity |
| :--- |
| - score : Real |
| + setScore(s : Real) |
| + getScore() : Real |
| + getGrade() : String |

## 类列表 14-8

```
1 Class GradedActivity
2 // score 字段存储一个数值分数。
3 Private Real score
4
5 // 变异器 (Mutator)
6 Public Module setScore(Real s)
7 Set score = s
8 End Module
9
10 // 访问器 (Accessor)
11 Public Function getScore()
12 Return score
13 End Function
14
15 // getgrade 方法
16 Public Function getGrade()
17 // 用于存储等级的局部变量。
18 Declare String grade
19
20 // 确定等级。
21 If score >= 90 Then
22 Set grade = "A"
23 Else If score >= 80 Then
24 Set grade = "B"
25 Else If score >= 60 Then
26 Set grade = "C"
27 Else
28 Set grade = "D"
29 End If
30 // 返回等级。
31 Return the grade.
32 Return grade
33 End Function
34 End Class
```

## 程序 14-4

```
1 Module main()
2 // 用于存储测试分数的变量。
3 Declare Real testScore
4
5 // 用于引用
6 GradedActivity 对象的变量。
7 Declare GradedActivity test
8
9 // 创建一个 GradedActivity 对象。
10 Set test = New GradedActivity()
11
12 // 从用户处获取测试分数。
13 Display "Enter a numeric test score."
14 Input testScore
15
16 // 将分数存储在对象中。
17 test.setScore(testScore)
18
19 // 显示对象的等级。
20 Display "The grade for that test is " + 
21 test.getGrade()
22 End Module
```

## 程序输出（输入部分加粗显示）

Enter a numeric test score.
**89 [Enter]**The grade for that test is B

## 程序输出（输入部分加粗显示）

Enter a numeric test score.
**75 [Enter]**The grade for that test is C

蜜蜂和蝗虫是昆虫的特化版本

除了常见的昆虫特征外，蜜蜂还有自己独特的特征，例如蜇刺的能力。除了常见的昆虫特征外，蝗虫也有自己独特的特征，例如跳跃的能力。

所有昆虫都具有某些特征。

## 继承与“是一个”的关系

当一个对象是另一个对象的特化版本时，它们之间存在一种“是一个……”的关系。例如，蝗虫是一只昆虫。以下是几个“是一个……”的关系例子：

- * 贵宾是一只狗。
- 汽车是一辆交通工具。
- 花朵是一株植物。
- 矩形是一个形状。
- 足球运动员是一名运动员。

当对象之间存在“是一个……”的关系时，意味着特化对象具有泛化对象的所有特征，再加上使其变得特殊的额外特征。在面向对象编程中，继承被用于在类之间创建“是一个……”的关系。你可以通过创建另一个该类的特化版本类来扩展该类的功能。

继承涉及一个父类和一个子类。父类是泛化类，子类是特化类。你可以将子类类为父类的扩展版本。子类从父类继承字段和方法，而无需重写其中任何一个。此外，可以向子类中添加新的字段和方法，这使得它成为父类的特化版本。

> 注意：父类也称为基类（base classes），子类也称为派生类（derived classes）。这两组术语都是正确的。为了一致起见，本文将使用父类（superclass）和子类（subclass）术语。

让我们来看一个如何继承的示例。大多数老师会给学生布置各种评分活动。评分活动可以给出一个数值分数，如 70、85、90 等，以及一个字母等级，如 A、B、C、D 或 F。

图 14-18 显示了 GradedActivity 类的 UML 图，该类设计用于存储评分活动的数值分数。setScore 方法设置数值分数，getScore 方法返回数值分数。getgrade 方法返回与数值分数相对应的字母。类列表 14-8 显示了该类的伪代码。程序 14-4 中的伪代码演示了该类如何工作。

## 图 14-18 GradedActivity 类的 UML 图

| GradedActivity |
| :--- |
| - score : Real |
| + setScore(s : Real) |
| + getScore() : Real |
| + getGrade() : String |

## 类列表 14-8

```
1 Class GradedActivity
2 // score 字段存储一个数值分数。
3 Private Real score
4
5 // 变异器 (Mutator)
6 Public Module setScore(Real s)
7 Set score = s
8 End Module
9
10 // 访问器 (Accessor)
11 Public Function getScore()
12 Return score
13 End Function
14
15 // getgrade 方法
16 Public Function getGrade()
17 // 用于存储等级的局部变量。
18 Declare String grade
19
20 // 确定等级。
21 If score >= 90 Then
22 Set grade = "A"
23 Else If score >= 80 Then
24 Set grade = "B"
25 Else If score >= 60 Then
26 Set grade = "C"
27 Else
28 Set grade = "D"
29 End If
30 // 返回等级。
31 Return the grade.
32 Return grade
33 End Function
34 End Class
```

## 程序 14-4

```
1 Module main()
2 // 用于存储测试分数的变量。
3 Declare Real testScore
4
5 // 用于引用
6 GradedActivity 对象的变量。
7 Declare GradedActivity test
8
9 // 创建一个 GradedActivity 对象。
10 Set test = New GradedActivity()
11
12 // 从用户处获取测试分数。
13 Display "Enter a numeric test score."
14 Input testScore
15
16 // 将分数存储在对象中。
17 test.setScore(testScore)
18
19 // 显示对象的等级。
20 Display "The grade for that test is " + 
21 test.getGrade()
22 End Module
```

## 程序输出（输入部分加粗显示）

Enter a numeric test score.
**89 [Enter]**The grade for that test is B

## 程序输出（输入部分加粗显示）

Enter a numeric test score.
**75 [Enter]**The grade for that test is C

蜜蜂和蝗虫是昆虫的特化版本

除了常见的昆虫特征外，蜜蜂还有自己独特的特征，例如蜇刺的能力。除了常见的昆虫特征外，蝗虫也有自己独特的特征，例如跳跃的能力。

所有昆虫都具有某些特征。

## 继承与“是一个”的关系

当一个对象是另一个对象的特化版本时，它们之间存在一种“是一个……”的关系。例如，蝗虫是一只昆虫。以下是几个“是一个……”的关系例子：

- * 贵宾是一只狗。
- 汽车是一辆交通工具。
- 花朵是一株植物。
- 矩形是一个形状。
- 足球运动员是一名运动员。

当对象之间存在“是一个……”的关系时，意味着特化对象具有泛化对象的所有特征，再加上使其变得特殊的额外特征。在面向对象编程中，继承被用于在类之间创建“是一个……”的关系。你可以通过创建另一个该类的特化版本类来扩展该类的功能。

继承涉及一个父类和一个子类。父类是泛化类，子类是特化类。你可以将子类类为父类的扩展版本。子类从父类继承字段和方法，而无需重写其中任何一个。此外，可以向子类中添加新的字段和方法，这使得它成为父类的特化版本。

> 注意：父类也称为基类（base classes），子类也称为派生类（derived classes）。这两组术语都是正确的。为了一致起见，本文将使用父类（superclass）和子类（subclass）术语。

让我们来看一个如何继承的示例。大多数老师会给学生布置各种评分活动。评分活动可以给出一个数值分数，如 70、85、90 等，以及一个字母等级，如 A、B、C、D 或 F。

图 14-18 显示了 GradedActivity 类的 UML 图，该类设计用于存储评分活动的数值分数。setScore 方法设置数值分数，getScore 方法返回数值分数。getgrade 方法返回与数值分数相对应的字母。类列表 14-8 显示了该类的伪代码。程序 14-4 中的伪代码演示了该类如何工作。

## 图 14-18 GradedActivity 类的 UML 图

| GradedActivity |
| :--- |
| - score : Real |
| + setScore(s : Real) |
| + getScore() : Real |
| + getGrade() : String |

## 类列表 14-8

```
1 Class GradedActivity
2 // score 字段存储一个数值分数。
3 Private Real score
4
5 // 变异器 (Mutator)
6 Public Module setScore(Real s)
7 Set score = s
8 End Module
9
10 // 访问器 (Accessor)
11 Public Function getScore()
12 Return score
13 End Function
14
15 // getgrade 方法
16 Public Function getGrade()
17 // 用于存储等级的局部变量。
18 Declare String grade
19
20 // 确定等级。
21 If score >= 90 Then
22 Set grade = "A"
23 Else If score >= 80 Then
24 Set grade = "B"
25 Else If score >= 60 Then
26 Set grade = "C"
27 Else
28 Set grade = "D"
29 End If
30 // 返回等级。
31 Return the grade.
32 Return grade
33 End Function
34 End Class
```

## 程序 14-4

```
1 Module main()
2 // 用于存储测试分数的变量。
3 Declare Real testScore
4
5 // 用于引用
6 GradedActivity 对象的变量。
7 Declare GradedActivity test
8
9 // 创建一个 GradedActivity 对象。
10 Set test = New GradedActivity()
11
12 // 从用户处获取测试分数。
13 Display "Enter a numeric test score."
14 Input testScore
15
16 // 将分数存储在对象中。
17 test.setScore(testScore)
18
19 // 显示对象的等级。
20 Display "The grade for that test is " + 
21 test.getGrade()
22 End Module
```

## 程序输出（输入部分加粗显示）

Enter a numeric test score.
**89 [Enter]**The grade for that test is B

## 程序输出（输入部分加粗显示）

Enter a numeric test score.
**75 [Enter]**The grade for that test is C

蜜蜂和蝗虫是昆虫的特化版本

除了常见的昆虫特征外，蜜蜂还有自己独特的特征，例如蜇刺的能力。除了常见的昆虫特征外，蝗虫也有自己独特的特征，例如跳跃的能力。

所有昆虫都具有某些特征。

## 继承与“是一个”的关系

当一个对象是另一个对象的特化版本时，它们之间存在一种“是一个……”的关系。例如，蝗虫是一只昆虫。以下是几个“是一个……”的关系例子：

- * 贵宾是一只狗。
- 汽车是一辆交通工具。
- 花朵是一株植物。
- 矩形是一个形状。
- 足球运动员是一名运动员。

当对象之间存在“是一个……”的关系时，意味着特化对象具有泛化对象的所有特征，再加上使其变得特殊的额外特征。在面向对象编程中，继承被用于在类之间创建“是一个……”的关系。你可以通过创建另一个该类的特化版本类来扩展该类的功能。

继承涉及一个父类和一个子类。父类是泛化类，子类是特化类。你可以将子类类为父类的扩展版本。子类从父类继承字段和方法，而无需重写其中任何一个。此外，可以向子类中添加新的字段和方法，这使得它成为父类的特化版本。

> 注意：父类也称为基类（base classes），子类也称为派生类（derived classes）。这两组术语都是正确的。为了一致起见，本文将使用父类（superclass）和子类（subclass）术语。

让我们来看一个如何继承的示例。大多数老师会给学生布置各种评分活动。评分活动可以给出一个数值分数，如 70、85、90 等，以及一个字母等级，如 A、B、C、D 或 F。

图 14-18 显示了 GradedActivity 类的 UML 图，该类设计用于存储评分活动的数值分数。setScore 方法设置数值分数，getScore 方法返回数值分数。getgrade 方法返回与数值分数相对应的字母。类列表 14-8 显示了该类的伪代码。程序 14-4 中的伪代码演示了该类如何工作。

## 图 14-18 GradedActivity 类的 UML 图

| GradedActivity |
| :--- |
| - score : Real |
| + setScore(s : Real) |
| + getScore() : Real |
| + getGrade() : String |

## 类列表 14-8

```
1 Class GradedActivity
2 // score 字段存储一个数值分数。
3 Private Real score
4
5 // 变异器 (Mutator)
6 Public Module setScore(Real s)
7 Set score = s
8 End Module
9
10 // 访问器 (Accessor)
11 Public Function getScore()
12 Return score
13 End Function
14
15 // getgrade 方法
16 Public Function getGrade()
17 // 用于存储等级的局部变量。
18 Declare String grade
19
20 // 确定等级。
21 If score >= 90 Then
22 Set grade = "A"
23 Else If score >= 80 Then
24 Set grade = "B"
25 Else If score >= 60 Then
26 Set grade = "C"
27 Else
28 Set grade = "D"
29 End If
30 // 返回等级。
31 Return the grade.
32 Return grade
33 End Function
34 End Class
```

## 程序 14-4

```
1 Module main()
2 // 用于存储测试分数的变量。
3 Declare Real testScore
4
5 // 用于引用
6 GradedActivity 对象的变量。
7 Declare GradedActivity test
8
9 // 创建一个 GradedActivity 对象。
10 Set test = New GradedActivity()
11
12 // 从用户处获取测试分数。
13 Display "Enter a numeric test score."
14 Input testScore
15
16 // 将分数存储在对象中。
17 test.setScore(testScore)
18
19 // 显示对象的等级。
20 Display "The grade for that test is " + 
21 test.getGrade()
22 End Module
```

552 第14章 面向对象编程

注意 FinalExam 声明的第一行使用了 Extends 关键字，这表示该类扩展了另一个（父类）。父类的名称列在 extends 之后。所以，这表示 FinalExam 是类的名称，而 GradedActivity 是父类的名称。

如果我们想表达这两个类之间的关系，可以说 FinalExam 是 GradedActivity 类。

### 字段:
- numQuestions
- pointsEach
- numMissed

### 方法:
- Constructor
- getPointsEach
- getNumed
- setScore
- getScore
- getGrade

注意 score 字段没有在 FinalExam 类的成员列表中。这是因为 score 字段是私有的。父类的私有成员无法被子类访问，因此从技术上说，它们没有被继承。它们对于子类来说是真正的私有的。

为了看到继承在这个示例中是如何工作的，让我们仔细查看两个参数：考试题目的以及学生错的题目数量。在第 16 和 17 行，这些值被赋值给 numQuestions 和 numMissed 字段。在第 21 和 22 行，计算了每个题的分数和数值分数。在第 26 行，构造函数的最后一条语句如下：

```
call setScore(numericScore)
```

