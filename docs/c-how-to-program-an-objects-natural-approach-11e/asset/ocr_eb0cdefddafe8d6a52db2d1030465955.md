```
```cpp
1  // Fig05_17.cpp
2  // Unary scope resolution operator.
3  #include <iostream>
4  using namespace std;
5
6  const int number{7}; // global variable named number
7
8  int main() {
9      const double number{10.5}; // local variable named number
10
11     // display values of local and global variables
12     cout << "Local double value of number = " << number
13         << "\nGlobal int value of number = " << ::number << '\n';
14 }
```
```

```
```text
Local double value of number = 10.5
Global int value of number = 7
```
```

Fig. 5.17 | Unary scope resolution operator.

# ### Checkpoint

+   1. *(True/False)* The unary scope resolution operator can be used to access a local variable of the same name in an outer block.

Answer: False. Actually, the unary scope resolution operator cannot access local variables of the same name in outer blocks. It can be used only to access a global variable when a local variable of the same name is in scope.

# ### 5.19 Lnfylun Lhqtomh Wjtz Qarcv: Qjwazkrplm xzz Xndmwwqhlz

You probably noticed that the last Objectives bullet for this chapter, the last section name in the chapter outline, the last sentence in Section 5.1 and the section title above all look like gibberish. These are not mistakes! In this section, we continue our Objects-Natural presentation. You'll conveniently encrypt and decrypt messages with an object you create of a preexisting class that implements a Vigenère secret key cipher.²⁶

In previous Objects-Natural sections, you created objects of built-in C++ standard library class string and objects of classes from open-source libraries. Sometimes you'll use classes built by your organization or team members for internal use or for use in a specific project. For this example, we wrote our own Cipher class (in the header "cipher.h") and provided it to you.

For this Objects Natural section, we show you how easy it is to do encryption and decryption with an object of a pre-existing class. In Chapter 9, Custom Classes, you'll build custom classes. Section 9.22 explains the Vigenère secret key cipher algorithm and gives you the opportunity to study our custom class to see how it implements the cipher.

26. “Vigenère Cipher.” Wikipedia. Wikimedia Foundation. Accessed April 14, 2023, https://en.wikipedia.org/wiki/Vigenère_cipher.