
## 快速复习

- 1. 实例方法要求在访问之前必须实例化 `object`。

- 2. 私有成员只能在声明它们的 `class` 体内访问。

- 3. 在面向对象开发中，通常使用 `private` 修饰符定义数据，而访问这些数据的方法则声明为具有 `public` 访问权限。

- 4. 方法是描述数据行为的 `class` 成员。

- 5. 许多程序员采用使用动词短语作为方法名称的标准约定。

- 6. 重载方法是指名称相同但参数个数、类型或排列不同的 方法。例如，`DoSomething()` 方法被重载为以下签名：`public void DoSomething(int x, string y)` 和 `public void DoSomething(string y, int x)`。

- 7. 构造函数是创建 `class` 实例的特殊方法。构造函数不返回任何值——甚至不是 `void`。

- 8. 构造函数使用与 `class` 名称相同的标识符。关键字 `new` 用于调用构造函数。

- 9. 设计类时，通常对构造函数和大多数其他方法使用 `public` 访问修饰符，而对数据成员使用 `private` 访问修饰符。

- 10. 默认构造函数具有空体，如果你没有编写它，它会被自动创建。如果你编写了哪怕一个构造函数，你就会失去默认构造函数，并且必须自行编写它。

- 11. 访问器是用于访问 `private` 数据成员的方法。访问器也称为 getter 方法。

- 12. 修改器是用于更改 `object` 成员数据当前状态的方法。修改器方法也称为 setter。

- 13. 属性看起来像数据字段，并提供设置或获取 `private` 成员数据的方式。你可以只定义 set 而不定义 get，反之亦然。没有必要同时包含两者。

- 14. 要调用不返回值的方法，只需键入方法名称。如果它是 `static` 方法，则用 `class` 名称限定它。如果它是实例方法，则用 `object` 限定标识符。如果方法有参数，则调用中在括号内包含实际参数，不包含类型。

## 练习

- 1. 对象是 ________ 的实例。
  - a. 数据成员
  - b. 参数
  - c. 属性
  - d. 方法
  - e. 类

- 2. 属性是使用 ________ 访问模式定义的。
  - a. 公共
  - b. 静态
  - c. 私有
  - d. void
  - e. 受保护

- 3. 以下哪个修饰符限制最严格？
  - a. 私有
  - b. 静态
  - c. 公共
  - d. 内部
  - e. 受保护

- 4. 以下哪个标识符遵循类命名的标准命名约定？
  - a. Calculate Final Grade
  - b. MilesPerGallon
  - c. Students
  - d. Reports
  - e. Employee

- 5. 如果已从该类实例化了名为 `gradStudent` 的对象，以下哪种方式最适合调用 `Student` 类中定义的 `CalculateAvg()` 方法？

  ```
  public double CalculateAvg(double, double)
  ```

  - a. `gradStudent = CalculateAvg(87.2, 90);`
  - b. `answer = Student.CalculateAvg(87.2, 90);`
  - c. `CalculateAvg(87.2, 90);`
  - d. `answer = gradStudent.CalculateAvg(double, double);`
  - e. `answer = gradStudent.CalculateAvg(87.2, 90);`

- 6. 以下哪一个是从 `object` 类继承的用户定义方法之一？
  - a. `ToString()`
  - b. `Main()`
  - c. `CalculateAvg()`
  - d. `EqualsHashCode()`
  - e. `TypeHashCode()`

- 7. 属性与类的 __________ 相关，而方法与类的 __________ 相关。
  - a. 活动, 字段
  - b. 访问器, 修改器
  - c. 对象, 实例
  - d. 数据, 行为
  - e. 行为, 数据

- 8. 以下哪一个是 `CalculateAvg()` 的有效重载方法？

  ```
  int CalculateAvg(int val1, int val2)
  ```

  - a. `void CalculateAvg(int val1, int val2)`
  - b. `int CalculateAvg(int val1, int val2)`
  - c. `int CalculateAvg(double val1, double val2)`
  - d. `double CalculateAvg(int val1, int val2)`
  - e. `int CalculateAverage(int val2, int val1)`

- 9. 实例化类使用什么运算符？
  - a. 方法
  - b. 加号
  - c. `ToString()`
  - d. `new`
  - e. 等号

- 10. 实例变量与以下相同：
  - a. 私有成员数据
  - b. 局部变量
  - c. 属性
  - d. 实参
  - e. 形参

- 11. 给出下面所示的 `Employee` 类，以下哪一个是其默认构造函数的最合适签名？

  ```
  public class Employee {
  ```

  - a. `public void Employee()`
  - b. `public Employee()`
  - c. `public static Employee()`
  - d. `private void Employee()`
  - e. `private Employee()`

- 12. 以下可能是一个 ________ 的示例

  ```
  public double GetYards()
  ```

  - a. 构造函数
  - b. 修改器
  - c. 属性
  - d. 访问器
  - e. 类定义

- 13. 如果遵循标准 C# 命名约定，以下实例变量的属性名应为：

  ```
  private string name;
  ```

  - a. `propertyName`
  - b. `nameProperty`
  - c. `getName`
  - d. `name`
  - e. `Name`

- 14. 以下哪一个是对下面类的默认构造函数的有效调用？

  ```
  public class Employee {
  ```

  - a. `Employee employee1 = new Employee();`
  - b. `Employee employee1 = new undergrad();`
  - c. `Employee employee1;`
  - d. `Employee employee1 = new Employee(default);`
  - e. 信息不足，无法回答。

- 15. 给出以下类定义，修改器的有效签名是什么？

  ```
  public class Student {
      private string name;
      private double gpa;
  }
  ```

  - a. `public double SetGpa(double gpaValue)`
  - b. `public void SetGpa(double gpaValue)`
  - c. `public double SetGpa()`
  - d. `public void GetGpa(double gpaValue)`
  - e. `public double SetGpa()`

- 16. 在 UML 类图中
  - a. 类名出现在图的底部区域
  - b. 数据成员显示 + 表示公共访问
  - c. 方法不显示
  - d. 类的对象出现在图的中间区域
  - e. 方法在图上显示返回类型

- 17. C# 中以下哪个修饰符与构造函数一起使用？
  - a. `const`
  - b. `private`
  - c. `public`
  - d. `static`
  - e. `protected`

- 18. 通常，成员数据使用 ________ 访问修饰符，而面向对象解决方案中的方法使用 ________ 访问修饰符。
  - a. `protected, public`
  - b. `private, protected`
  - c. `public, protected`
  - d. `public, private`
  - e. `private, public`

- 19. 对于名为 `Account` 且具有 `accountNumber`、`balance` 和 `transactionAmount` 数据成员的类，减少当前余额中的交易金额的方法最合适的实例方法签名是什么？
  - a. `static double ReduceAccount(double accountBalance, double transactionAmount)`
  - b. `double ReduceAccount(double accountBalance, double transactionAmount)`
  - c. `static ReduceAccount()`
  - d. `void ReduceAccount()`
  - e. `static void ReduceAccount()`

- 20. 为了为 `ToString()` 方法提供新定义，方法签名中添加什么关键字？
  - a. `static`
  - b. `override`
  - c. `new`
  - d. `overload`
  - e. `public`

- 21. 给出以下代码片段：

  ```csharp
  public class Camera
  {
      private double zoom;
      private double lensSpeed;
      public double Zoom
      {
          get
          {
              return zoom;
          }
      }
      public Camera()
      {
      }
      public Camera(double zCapacity, double ls)
      {
          int xValue = 2;
          zoom = zCapacity * xValue;
          lensSpeed = ls;
      }
      public double GetLensSpeed()
      {
          return lensSpeed;
      }
  }
  ```

  识别以下项目对应的行号：

  - a. 方法签名
  - b. 属性标识符
  - c. 默认构造函数
  - d. 形式参数
  - e. 局部变量

- 22. 解释实例方法与类方法有何不同。调用每种不同类型时有什么不同？哪一种需要在调用时要求一个对象？

- 23. 重写方法是什么意思？为什么应该为用户定义的类重写 `ToString()` 方法？

- 24. 解释构造函数的角色。什么是默认构造函数？在什么情况下会自动获得默认构造函数？
