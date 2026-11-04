same with the name of the class. If using the javac compiler, we write in the command line:

```
javac MainClass.java
```

The compilation produces the bytecode file MainClass.class, which is executed by writing in the command line:

```
java MainClass
```

Let’s explain the program sentences. Since Java is an object-oriented language, it allows us to define our own classes. In our program, we defined the class MainClass. The general form to define a class is as follows:

```
A_M N_A_M class class_name {
    A_M N_A_M class_field;
    A_M N_A_M class_field;
    ...
    A_M class_constructor;
    A_M class_constructor;
    ...
    A_M N_A_M class_method {
    ...
    }
    A_M N_A_M class_method {
    ...
    }
    ...
}
```

A_M and N_A_M stand for Access Modifier and Non Access Modifier, respectively, and they are optional. We can omit either one of them or both, as we did in our MainClass. We’ll talk later about modifiers and constructors, so forget them for now.

As in C/C++, the existence of main() is mandatory. However, unlike C/C++, main() should be implemented as a method of a class. Just for your information, a Java program can have more than one main() method. In Java, every function defined within a class is called a method of the class. In contrast to C++, Java methods must be implemented within the class. The member variables defined within a class are called fields of the class.

The public keyword is one of the available Access Modifiers and declares that this class can be accessed by another class. The static keyword is one of the available Non Access Modifiers and declares that main() can be invoked even if no instance of the class in which it is contained has been created, that is, an instance of the MainClass class in our example. We’ll discuss more about the public and static keywords later.

As in C/C++, the void keyword before the method’s name declares that no value is returned. In contrast to C/C++, you are not allowed to use the void keyword inside the parentheses to declare that the method does not accept parameters. In Java, we just leave the parentheses empty. To end with the first line of the program, the args[] parameter is an array of instances of the class String, which is one of the native classes provided by Java and it is used for string manipulation. The role of args[] is similar to the argc and argv[] parameters in C/C++; that is, it serves to pass data to main() from the command line. The class System is another one Java native class, while out is one of its static fields