# Chapter 13 Class Inheritance

# Showing Virtual Method Behavior

In Listing 13.9 the methods are invoked by objects, not pointers or references, so this program does not use the virtual method feature. Let's look at an example for which the virtual methods do come into play. Suppose you would like to manage a mixture of Brass and BrassPlus accounts. It would be nice if you could have a single array that holds a mixture of Brass and BrassPlus objects, but that's not possible. Every item in an array has to be of the same type, and Brass and BrassPlus are two separate types. However, you can create an array of pointers-to-Brass. In that case, every element is of the same type, but because of the public inheritance model, a pointer-to-Brass can point to either a Brass or a BrassPlus object. Thus, in effect, you have a way of representing a collection more than one type of object with a single array. This is polymorphism, and Listing 13.10 shows a simple example.

Listing 13.10 usebase2.cpp

```
// usebase2.cpp -- polymorphic example
// compile with brass.cpp
#include <iostream>
#include <string>
#include "brass.h"
int CLIENTS = 4;

int main()
{
    using std::cin;
    using std::cout;
    using std::endl;

    Brass * p_clients[CLIENTS];
    string tempname;
    long tempnum;
    double tempbal;
    char kind;

    for (int i = 0; i < CLIENTS; i++)
    {
        cout << "Enter client's name: ";
        getline(cin,temp);
        cout << "Enter client's account number: ";
        cin >> tempnum;
        cout << "Enter opening balance: ";
        cin >> tempbal;
        cout << "Enter 1 for Brass Account or ";
        cout << "2 for BrassPlus Account: ";
        while (cin >> kind && (kind != '1' && kind != '2'))
            cout << "Enter either 1 or 2: ";
    }

```