# Pointers in C++

# 4.1  Introduction

After you work through this chapter, it is hoped that you might feel a little more confident about using pointers in C++. What exactly is a pointer? In programming terms, a pointer is a variable pointing towards the memory space or the address of a given variable. A pointer holds the address of the very first byte of the memory location where it is pointing to. This first byte address is called the base address, and it is like a variable used to store the address of another variable.

The concept of pointers takes time and effort to understand, but keep practicing your coding skills while using them. With some effort, pointers can play an important role in helping you make part of your code faster and easier to access. You can do some important actions with pointers, even declaring a pointer to a pointer. Let’s start with the basic declaration and initializing process for pointers.

# 4.2  Pointers: Declaration and Initialization

Let’s start with the basics. The & (ampersand) is used to make reference to the memory location of another variable. Pointers can be dereferenced, which we do with the * (asterisk), and this means the operator gets the value of the variable. The following code snippet declares a variable of type pointer.