# 4.2 Destructors

The destructor gets called for each object that is about to go out of scope. It appears as a member function of class whether we define it or not. It has the same name as that of the class prefixed with a tilde sign. It does not take parameters. It does not return anything (not even void). The prototype of a destructor is

```
~class name>();
```

The need for a function that guarantees deinitialization of member data of a class and frees resources acquired by the object during its lifetime will be explained soon. Destructors fulfill this.

The compiler embeds a call to the destructor for every object when it is destroyed. We have one more look at the main() function of Listing 4.1.

```
void main()
{
nA AI;
} //AI goes out of scope before the main() function terminates.
```

The compiler embeds a call to the destructor for 'AI1'. It embeds the following.

```
A1~A1(); //destructor called not legal C++ code
```



-A(&A1); //see chapter 2

The destructor will also be called for an object that has been created in the heap just before the delete operator is applied on the pointer pointing it.

```
A * APtr;
APtr = new A; //object created constructor called
.\.
delete APtr; //object destroyed destructor called
```



APtr->~APtr(); //destructor called for *APtr
delete APtr; //memory for *APtr released



~A(APtr); //see the section on 'this' pointer in Chapter 2

Unlike its name, the destructor does not 'destroy' or deactivate an object that occupies. It is merely a member function that is called for each object before the object goes out of scope (destroyed).

As can be readily observed, the compiler embeds a call to the destructor for every every object that is going out of scope. But we did not prototype and define the destructor inside the class. Then was the above call to the destructor resolved? The compiler prototypes and defines the destructor for us. But what statements the definition of such a destructor have? The answer is 'nothing'. An example of a compiler-defined destructor follows.