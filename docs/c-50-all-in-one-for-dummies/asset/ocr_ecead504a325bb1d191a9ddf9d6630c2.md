Well-written code with rules that the compiler can enforce saves everyone from the occasional bullet to the big toe.

Before you get too excited, however, notice that the program doesn’t build. Attempts to do so generate this error message:

```
'BankAccount.BankAccount._balance' is inaccessible due to its protection level.
```

I don’t know why it doesn’t just come out and say, “Hey, this is private, so keep your mitts off.” The statement ba._balance += 10; is illegal because _balance isn’t accessible to Main(), a method outside the BankAccount class. Replacing this line with ba.Deposit(10) solves the problem. The BankAccount.Deposit() method is public and therefore accessible to Main() and other parts of your program.

Not declaring a class member’s access type explicitly is the same as declaring it private.

The default access type is private. However, you should include the private keyword to remove any doubt. Good programmers make their intentions explicit, which is another way to reduce errors.

# Jumping ahead — other levels of security

Understanding this section depends on your having some knowledge of inheritance (see Chapter 6 in this minibook) and namespaces (Chapter 10 in this minibook). You can skip this section for now if you want, but just know that it’s here when you need it.

C# provides these levels of security:

+   ♦ A public member is accessible to any class in the program.
♦ A private member is accessible only from the current class.
♦ A protected member is accessible from the current class and any of its subclasses.
♦ An internal member is accessible from any class within the same program module or assembly.

A C# “module,” or assembly, is a separately compiled piece of code, either an executable program in an .EXE file or a supporting library module in a .DLL file. A single namespace can extend across multiple assemblies. (Chapter 10 in this minibook explains C# assemblies and namespaces and discusses access levels other than public and private.)

+   ♦ An internal protected member is accessible from the current class and any subclass, and from classes within the same module.