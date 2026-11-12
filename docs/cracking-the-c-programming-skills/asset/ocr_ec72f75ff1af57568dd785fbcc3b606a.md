# # 1 C VERSUS C++

This chapter will cite the most important differences between C and C++. It is also to be noted that ‘C’ language is top down language whereas ‘C++’ is a bottom up one. At the end of this chapter, you will be knowing the important and elementary vicissitudes to be handled carefully while moving into C++ from C language.

+   1. What is the output of the code? (L2)
+   
+   ~~~cpp
+   #include<iostream.h>
+   void main()
+   { cout<< “hello world”;}
+   ~~~
+   
+   (a) hello world
+   (b) hello
+   (c) Unpredictable
+   (d) Compiler dependent
+   
+   **Answer:** (d) ‘cout’ is the function used for printing output in ‘C++’. The operator ‘<<’ is called extraction operator. It is used for extracting the value from the right side, and gives it to the console. In ‘g++’ it gives error. Whereas in other compilers and some older versions it might give ‘hello world’.

+   2. What will be error thrown by the code? (L4)
+   
+   ~~~cpp
+   #include<iostream.h>
+   void main()
+   { cout<< “hello world”;}
+   ~~~
+   
+   (a) Fatal error: iostream.h: no such file or directory
+   (b) ‘::main()’ must return ‘int’
+   (c) ‘cout’ was not declared in this scope
+   (d) All of the above
+   
+   **Answer:** (a) A fatal error terminates compilation. Then no other errors will be thrown. This is because ‘g++’ doesn’t support this way of compilation.

+   3. What will be error thrown by the code? (L3)
+   
+   ~~~cpp
+   #include<iostream>
+   using namespace std;
+   void main()
+   { cout<< “hello world”;}
+   ~~~
+   
+   (a) Fatal error: iostream.h: no such file or directory
+   (b) ‘::main()’ must return ‘int’
+   (c) ‘cout’ was not declared in this scope
+   (d) No error
+   
+   **Answer:** (b) ‘using namespace std’ is for handling naming collisions and adding external files and definition. This doesn’t exist in ‘C’. It is used to prevent collisions while naming memory spaces. Initially, it was used only on system with multiple users and shared memory, but now it has been adapted as a mandatory syntax in ‘G++’. Also in ‘G++’ the default ‘main’ must be of ‘int’ type and not ‘void’. Thus, the error. But it is also to be noted that the compiler doesn’t throw any error or warning even if there is no return statement given at the end of ‘main’.

+   4. What will be error thrown by the code? (L4)
+   
+   ~~~cpp
+   #include<iostream>
+   int main()
+   { std::cout<< “hello world”;}
+   ~~~