
The code begins by creating a `typedef` called `GobMember`, as discussed earlier in this section. It then creates a method pointer, `func`, to access the method. When using C++11 or above, you can replace these two lines with the much easier-to-understand single line:

```cpp
auto func = &Gobstopper::Chew;
```

Of course, when you use this alternative, the compiler must deduce the correct types, which it may not always do correctly. Using the `typedef` gives you additional control at the cost of complexity.

The code then creates two instances of `Gobstopper`, `inst` and another. In both cases, it directly assigns a value to `WhichGobstopper`, which will vary depending on instance and accessed through this. The final section calls the `Chew()` method indirectly using `func` in each instance and assigns a name as the input string.

When you run the code, you can see from the output that it is indeed calling the correct method for each instance:

```text
10
Greg W.
20
Jennifer W.
```

Now, when you hear “the correct method for each instance,” what the statement really means is that the code is calling the same method each time but using a different instance. If you’re thinking in object-oriented terms, consider each instance as having its own copy of the method. Therefore it’s okay to say “the correct method for each instance.”

## Pointing to static methods

A *static method* is, in many senses, just a plain old function. The difference is that you have to use a class name to call a static function. But remember that a static method does not go with any particular instance of a class; therefore you don’t need to specify an instance when you call the static function.

Here’s an example class (as shown in the `FunctionPointer03` example) with a static function:

```cpp
class Gobstopper {
public:
  static string MyClassName() {
    return "Gobstopper!";
  }
  int WhichGobstopper;
  int Chew(string name) {
    cout << WhichGobstopper << endl;
    cout << name << endl;
    return WhichGobstopper;
  }
};
```

And here’s some code that takes the address of the static function and calls it by using the address:

```cpp
int main() {
  typedef string (*StaticMember)();
  StaticMember staticfunc = &Gobstopper::MyClassName;
  cout << staticfunc() << endl;
  return 0;
}
```

Note that the call `staticfunc()` doesn’t refer to a specific instance and it doesn’t refer to the class, either. The application just called it. Because the truth is that deep down inside, the static function is just a plain old function.

## Referring to References

This section discusses how to use references and assumes that you already know how to pass a parameter by reference when you’re writing a function. (For more information about passing parameters by reference, see Book 1, Chapter 8.) But you can use references for more than just parameter lists. You can declare a variable as a reference type. And just like job references, this use of references can be both good and devastating. So be careful when you use them.

### Reference variables

Declaring a variable that is a reference is easy. Whereas the pointer uses an asterisk, *, the reference uses an ampersand, &. But it has a twist. You can’t just declare it, like this:

```cpp
int &BestReference; // Nope! This won't work!
```

If you try this, you see an error that says `BestReference declared as reference but not initialized`. That sounds like a hint: Looks like you need to initialize it.

Yes, references need to be initialized. As the name implies, *reference* refers to another variable. Therefore, you need to initialize the reference so that it refers to some other variable, like so (as shown in the `Reference01` example):

```cpp
int ImSomebody;
int &BestReference = ImSomebody;
```

From this point on, the variable `BestReference` refers to — that is, is an *alias* for — `ImSomebody`. So, if you change the value of `BestReference`, as shown here:

```cpp
BestReference = 10;
```

you’ll really be setting `ImSomebody` to 10. Look at this code that could go inside `main()`:

```cpp
int ImSomebody;
int &BestReference = ImSomebody;
BestReference = 10;
cout << ImSomebody << endl;
```

When you run this code, you see the output

```text
10
```

That is, setting `BestReference` to 10 caused `ImSomebody` to change to 10, which you can see when you print the value of `ImSomebody`. That’s what a reference does: It refers to another variable.

![](img/128ab511de4e7360e167e3b15cdd5dd0_530_0.png)

Because a reference refers to another variable, that implies that you can’t have a reference to just a number, as in `int &x=10`. In fact, the offending line has been implicated: You are not allowed to do that. You can have only a reference that refers to another variable.

### Returning a reference from a function

It’s possible to return a reference from a function. But be careful if you try to do this: You don’t want to return a reference to a local variable within a function, because when the function ends, the storage space for the local variables goes away.

But you can return a reference to a global variable. Or, if the function is a method, you can return a reference to a property.

For example, here’s a class found in the `Reference02` example that has a function that returns a reference to one of its variables:

```cpp
class DigInto {
private:
    int secret;
public:
    DigInto() { secret = 150; }
    int &GetSecretVariable() { return secret; }
    void Write() { cout << secret << endl; }
};
```

Notice that the constructor stores 150 in the secret variable, which is private. The GetSecretVariable() function returns a reference to the private variable called secret. The Write() function writes out the value of the secret variable. Lots of secrets here! And some surprises, too, which you discover shortly. You can use this class like so:

```cpp
int main()
{
    DigInto inst;
    inst.Write();

    int &pry = inst.GetSecretVariable();
    pry = 30;
    inst.Write();

    auto &pry2 = inst.GetSecretVariable();
    pry2 = 40;
    inst.Write();
    return 0;
}
```

The example uses two kinds of references, one int and one auto (you must have C++ 11 or above installed to use the second type). Notice that using auto doesn’t eliminate the need for the & to create a reference. If you were to write auto pry2 = inst.GetSecretVariable(); instead, you’d receive a warning message stating warning: variable 'pry2' set but not used. However, the code would still compile, and if you use the Build➔Build and Run option, you might not even notice the warning.

When you run this example, you see the following output:

```text
150
30
40
```

Here’s a look at the code in a little more detail. The first output line is the value in the secret variable right after the application creates the instance. But look at the code carefully: The variable called pry is a reference to an integer, and it gets the results of GetSecretVariable(). What is that result? It’s a reference to the private variable called secret — which means that pry itself is now a reference to that variable. Yes, a variable outside the class now refers directly to a private member in the instance! After that, the code sets pry to 30. When the code calls Write() again, the private variable will indeed change. (The same sequence occurs when you use the auto variable pry2.)

Creating code like this is a bad idea because it provides access to a private variable. The GetSecretVariable() function pretty much wipes out any sense of the variable’s actually remaining private. The main() function is able to grab a reference to it and poke around and change it however it wanted, as if it were not private!

That’s a problem with references: They can potentially leave your code wide open. Therefore, think twice before returning a reference to a variable. Here’s one of the biggest risks: Somebody else may be using this code, may not understand references, and may not realize that the variables called pry and pry2 have a direct link to the private secret variable. Such an inexperienced programmer might then write code that uses and changes pry or pry2 — without realizing that the property is changing along with it. Later on, then, a bug results — a pretty nasty one at that!

![](img/128ab511de4e7360e167e3b15cdd5dd0_532_0.png)

TIP

Because functions returning references can leave unsuspecting and less-experienced C++ programmers with just a wee bit too much power on their hands, it’s a best practice to use caution with references. No, you don’t have to avoid them altogether; it’s simply a good idea to be careful. Use them only if you really feel you must. But remember also that a better approach in classes is to have member access functions that can guard the private variables.

However, now that you’ve received the usual warnings, know that references can be very powerful, provided that you understand what they do. When you use a reference, you can easily modify another variable without having to go through pointers — which can make life much easier sometimes. So, please: Use your newfound powers carefully.

## Working with Arrays, Pointers, and References
