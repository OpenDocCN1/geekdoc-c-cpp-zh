# 296 CHAPTER 7 Constructors and Other Tools

Note that the only difference is that we made the parameter call-by-reference by adding & we added the const modifiers. If there is a function declaration, then the same change must be made to the parameters in the function declaration.

Constant parameters are a form of automatic error checking. If your function definition contains a mistake that causes an inadvertent change to the constant parameter, the compiler will issue an error message.

The parameter const can be used with any kind of parameter; however, it is normally used only for call-by-reference parameters for classes (and for certain other parameters whose arguments are large, such as arrays).

Suppose you invoke a member function for an object of a class, such as the class BankAccount in Display 7.2. For example,

```
BankAccount myAccount;
myAccount.input(\);
myAccount.output();
```

The invocation of the member function input changes the values of the member variables in the calling object myAccount. The calling object behaves sort of like call-by-reference parameter; the function invocation can change the calling object. Sometimes, you do not want the member function output should not change the values of the calling object's member variables. You can use the const modifier to tell the compiler that a member function invocation should not change the calling object.

# const with member functions

The modifier const applies to calling objects in the same way that it applies to parameters. If you have a member function that should not change the value of a calling object, you can mark the function with the const modifier; the computer will issue an error message if your function code inadvertently changes the value of the calling object. In the case of a member function, the const goes at the end of the function declaration, just before the final semicolon, as shown next:

```
class BankAccount{
public:
  ...
  void output() const;
  ...
```

The modifier const should be used in both the function declaration and the function definition, so the function definition for output would begin as follows:

```
void BankAccount::output() const{
  ...
```

The remainder of the function definition would be the same as in Display 7.2.