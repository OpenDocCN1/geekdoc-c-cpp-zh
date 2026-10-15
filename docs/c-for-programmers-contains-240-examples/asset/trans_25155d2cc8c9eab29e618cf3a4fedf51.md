
```
19 // set base salary
20 void BasePlusCommissionEmployee::setBaseSalary( double salary )
21 {
22     baseSalary = ( salary < 0.0 ) ? 0.0 : salary;
23 } // end function setBaseSalary
24
25 // return base salary
26 double BasePlusCommissionEmployee::getBaseSalary() const
27 {
28     return baseSalary;
29 } // end function getBaseSalary
30
31 // calculate earnings
32 double BasePlusCommissionEmployee::earnings() const
33 {
34     // derived class cannot access the base class's private data
35     return baseSalary + ( commissionRate * grossSales );
36 } // end function earnings
37
38 // print BasePlusCommissionEmployee object
39 void BasePlusCommissionEmployee::print() const
40 {
41     // derived class cannot access the base class's private data
42     cout << "base-salaried commission employee: " << firstName << ' '
43         << lastName << "\nsocial security number: " << socialSecurityNumber
44         << "\ngross sales: " << grossSales
45         << "\ncommission rate: " << commissionRate
46         << "\nbase salary: " << baseSalary;
47 } // end function print
```

C:\cppfp_examples\ch12\Fig12_10_11\BasePlusCommissionEmployee.cpp(35) :
error C2248: 'CommissionEmployee::commissionRate' :
    cannot access private member declared in class 'CommissionEmployee'
    C:\cppfp_examples\ch12\Fig12_10_11\CommissionEmployee.h(37) :
    see declaration of 'CommissionEmployee::commissionRate'
    C:\cppfp_examples\ch12\Fig12_10_11\CommissionEmployee.h(10) :
    see declaration of 'CommissionEmployee'

C:\cppfp_examples\ch12\Fig12_10_11\BasePlusCommissionEmployee.cpp(35) :
error C2248: 'CommissionEmployee::grossSales' :
    cannot access private member declared in class 'CommissionEmployee'
    C:\cppfp_examples\ch12\Fig12_10_11\CommissionEmployee.h(36) :
    see declaration of 'CommissionEmployee::grossSales'
    C:\cppfp_examples\ch12\Fig12_10_11\CommissionEmployee.h(10) :
    see declaration of 'CommissionEmployee'

C:\cppfp_examples\ch12\Fig12_10_11\BasePlusCommissionEmployee.cpp(42) :
error C2248: 'CommissionEmployee::firstName' :
    cannot access private member declared in class 'CommissionEmployee'
    C:\cppfp_examples\ch12\Fig12_10_11\CommissionEmployee.h(33) :
    see declaration of 'CommissionEmployee::firstName'
    C:\cppfp_examples\ch12\Fig12_10_11\CommissionEmployee.h(10) :
    see declaration of 'CommissionEmployee'

Fig. 12.11 | BasePlusCommissionEmployee implementation file: private base-class data cannot be accessed from derived class. (Part 2 of 3.)

```
C:\cppfp_examples\ch12\Fig12_10_11\BasePlusCommissionEmployee.cpp(43) :
error C2248: 'CommissionEmployee::lastName' :
    cannot access private member declared in class 'CommissionEmployee'
    C:\cppfp_examples\ch12\Fig12_10_11\CommissionEmployee.h(34) :
    see declaration of 'CommissionEmployee::lastName'
    C:\cppfp_examples\ch12\Fig12_10_11\CommissionEmployee.h(10) :
    see declaration of 'CommissionEmployee'

C:\cppfp_examples\ch12\Fig12_10_11\BasePlusCommissionEmployee.cpp(43) :
error C2248: 'CommissionEmployee::socialSecurityNumber' :
    cannot access private member declared in class 'CommissionEmployee'
    C:\cppfp_examples\ch12\Fig12_10_11\CommissionEmployee.h(35) :
    see declaration of 'CommissionEmployee::socialSecurityNumber'
    C:\cppfp_examples\ch12\Fig12_10_11\CommissionEmployee.h(10) :
    see declaration of 'CommissionEmployee'

C:\cppfp_examples\ch12\Fig12_10_11\BasePlusCommissionEmployee.cpp(44) :
error C2248: 'CommissionEmployee::grossSales' :
    cannot access private member declared in class 'CommissionEmployee'
    C:\cppfp_examples\ch12\Fig12_10_11\CommissionEmployee.h(36) :
    see declaration of 'CommissionEmployee::grossSales'
    C:\cppfp_examples\ch12\Fig12_10_11\CommissionEmployee.h(10) :
    see declaration of 'CommissionEmployee'

C:\cppfp_examples\ch12\Fig12_10_11\BasePlusCommissionEmployee.cpp(45) :
error C2248: 'CommissionEmployee::commissionRate' :
    cannot access private member declared in class 'CommissionEmployee'
    C:\cppfp_examples\ch12\Fig12_10_11\CommissionEmployee.h(37) :
    see declaration of 'CommissionEmployee::commissionRate'
    C:\cppfp_examples\ch12\Fig12_10_11\CommissionEmployee.h(10) :
    see declaration of 'CommissionEmployee'
```

Fig. 12.11 | BasePlusCommissionEmployee implementation file: private base-class data cannot be accessed from derived class. (Part 3 of 3.)

## Common Programming Error 12.1

> 如果派生类构造函数调用其基类构造函数时传递的参数与基类构造函数定义中指定的参数个数和类型不一致，则会发生编译错误。

## Performance Tip 12.1

> 在派生类构造函数中，通过成员初始化列表显式初始化成员对象并调用基类构造函数，可以防止重复初始化，即先调用默认构造函数，然后在派生类构造函数体中再次修改数据成员。

编译器对图 12.11 中第 35 行生成错误，是因为基类 CommissionEmployee 的数据成员 commissionRate 和 grossSales 是私有的——派生类 BasePlusCommissionEmployee 的成员函数不允许访问基类 CommissionEmployee 的私有数据。请注意，我们在图 12.11 中使用粗体黑色文本标出了错误代码。编译器还在 BasePlusCommissionEmployee 的 print 成员函数的第 42–45 行发出额外的错误，原因相同。正如你所见，C++ 严格执行对私有数据成员访问的限制，因此即使派生类与其基类密切相关，也无法访问基类的私有数据。

[注：为节省篇幅，我们在此示例中仅展示了 Visual C++ 2005 的错误信息。你的编译器产生的错误信息可能与此处所示不同。还请注意，我们在冗长的错误信息中用粗体突出了关键部分。] 我们故意在图 12.11 中包含错误代码，以强调派生类的成员函数不能访问其基类的私有数据。BasePlusCommissionEmployee 中的错误本可以通过使用从类 CommissionEmployee 继承的 get 成员函数来避免。例如，第 35 行本可以调用 getCommissionRate 和 getGrossSales 分别访问 CommissionEmployee 的私有数据成员 commissionRate 和 grossSales。类似地，第 42–45 行本可以使用适当的 get 成员函数检索基类数据成员的值。在下一个示例中，我们将展示使用 protected 数据如何避免在此示例中遇到的错误。

## 使用 #include 在派生类头文件中包含基类头文件

请注意，我们在派生类头文件中 #include 了基类的头文件（图 12.10 的第 10 行）。这是出于三个原因。第一，为了让派生类在第 12 行使用基类的名称，我们必须告诉编译器基类存在——CommissionEmployee.h 中的类定义正是这样做的。

第二个原因是编译器使用类定义来确定该类对象的大小（如我们在第 3.8 节中讨论的）。创建该类对象的客户端程序必须 #include 类定义，以便编译器为对象保留适当量的内存。在使用继承时，派生类对象的大小取决于其类定义中显式声明的数据成员以及从其直接和间接基类继承的数据成员。第 10 行包含基类定义使编译器能够确定基类的数据成员作为派生类对象的一部分所需的内存，以及由此对派生类对象总大小的贡献。

第 10 行的最后一个原因是允许编译器确定派生类是否正确使用了基类继承的成员。例如，在图 12.10–12.11 的程序中，编译器使用基类头文件确定派生类访问的数据成员在基类中是私有的。由于这些成员对派生类不可访问，编译器会生成错误。编译器还使用基类的函数原型来验证派生类对继承自基类的函数的调用——你将在图 12.16 中看到此类函数调用的示例。

## 继承层次结构中的链接过程

在第 3.9 节中，我们讨论了创建可执行 GradeBook 应用程序的链接过程。在该示例中，你看到客户端的对象代码与类 GradeBook 的对象代码以及客户端代码或类 GradeBook 中使用的任何 C++ 标准库类的对象代码链接在一起。

使用继承层次结构中的类的程序的链接过程是类似的。该过程需要程序中使用的所有类的对象代码，以及程序中使用的任何派生类的直接和间接基类的对象代码。假设客户端想要创建一个使用类 BasePlusCommissionEmployee 的应用程序，该类是 CommissionEmployee 的派生类（我们将在第 12.4.4 节看到一个示例）。在编译客户端应用程序时，客户端的对象代码必须与类 BasePlusCommissionEmployee 和 CommissionEm- 的对象代码链接

