# Chapter 10 Objects and Classes

example, is 1 byte of memory, and a double is often 8 bytes of memory. But a little reflection leads you to conclude that a data type is also defined in terms of the operations that can be performed on it. For example, the int type can use all the arithmetic operations. You can add, subtract, multiply, and divide integers. You can also use the modulus operator (\%) with them.

+   * It determines how much memory is needed for a data object.
* It determines how the bits in memory are interpreted. (A long and float use the same number of bits in memory, but they are translated into numeric values differently.)
* It determines what operations, or methods, can be performed using the data object.

For built-in types, the information about operations is built in the compiler. When you define a user-defined type in C++, you have to provide the same kind of information yourself. In exchange for this extra work, you gain the power and flexibility to custom your new data types to match real-world requirements.

# Classes in C++

A class is a C++ vehicle for translating an abstraction to a user-defined type. It combines data representation and methods for manipulating that data into one package. Look at a class that represents stocks.
First, you have to think a bit about how to represent stocks. You could take one share of stock as the basic unit and define a class to represent a share. However, that implies that you would need 100 objects to represent 100 shares, and that's not practical. Instead, you can represent a person's current holdings in a particular stock as a basic unit. The number of shares would be part of the data representation. A realistic approach would have to maintain records of such things as initial purchase price and date of purchase for tax purposes. It would also have to manage events like stock splits. This seems a bit ambitious for a first effort at idealized view of matters. In particular, you can limit the operations you perform to the following:

+   * Acquire stock in a company.
* Buy more shares of the same stock.
* Sell stock.
* Update the per-share value of a stock.
* Display information about the holdings.