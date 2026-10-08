# 264 Restricting Access to Class Members

![](bbox=[0.144, 0.111, 0.215, 0.169])

Well-written code with rules that the compiler can enforce everyone from the occasional bullet to the big toe.

Before you get too excited, notice that the program doesn't build. Attempts to do generate this error message:

```
'BankAccount.BankAccount._balance' is inaccessible due to its protection level.
```

I don't know why it doesn't just come out and, "Hey, this is private, keep your mitt off." The statement ba\_balance += 10; is illegal because\_balance is inaccessible to Main(), a method outside the BankAccount class. Replacing this line with ba.Deposit(10) solves the problem. The BankAccount.Deposit() method is public and therefore accessible to Main() and other parts of your program.

![](bbox=[0.144, 0.345, 0.215, 0.403])

Not declaring a class member's access type explicitly is the same as declaring it.

![](bbox=[0.144, 0.444, 0.215, 0.502])

The default access type is private. However, you should include the private key to remove any doubt. Good programmers make their intent explicit, which is another way to reduce errors.

# Jumping head — other levels of security

Understanding this section depends on your having some knowledge of inheritance (see Chapter 6 in this minibook) and namespaces (Chapter 10 in this minibook). You can skip this section for if you want, but just know that's here when you need it.

C# provides these levels of security:

+   * A public member is accessible to any class in the program.
* A private member is accessible only from the current class.
* A protected member is accessible from the current class and any of its subclasses.
* An internal member is accessible from any class within the same program or assembly.

C# "module", or assembly, is a separately compiled piece of code. either an executable program in an .EXE file or a supporting library module in .DLL file. A single namespace can extend across assemblies (Chapter 10 in this minibook explains C# assemblies and namespaces and discusses access levels other than public and private.)

![](bbox=[0.144, 0.773, 0.215, 0.831])

+   * An internal protected member is accessible from the current class and any subclass, and from classes within the same module.