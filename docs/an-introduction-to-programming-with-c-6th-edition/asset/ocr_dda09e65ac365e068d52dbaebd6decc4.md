The IPO chart in Figure 3-3 contains a total of five input, processing, and output items. Therefore, five memory locations will be needed to store the values of the items. The memory locations will be variables, because each item's value should be allowed to vary during runtime. Figure 3-4 shows possible names (identifiers) for the variables.

| IPO chart item | Variable name |
|---|---|
| totalBill | totalBill |
| liquor charge | liquor |
| tip percentage | tipPercent |
| totalBill without liquor charge | totalNoLiquor |
| tip | tip |

Figure 3-4 Names of the variables for the Treyson Mobley problem

# # Mini-Quiz 3-1

+   1. How many items can a memory location store at a time?
2. Which of the following should be used in a C++ program to refer to the quantity variable?
   a. quantity
   b. QUANTITY
   c. Quantity
   d. All of the above.
3. Which of the following is a valid name for a memory location?
   a. jan.Sales
   b. 2ndQuarterIncome
   c. COMMISSION_RATE
   d. march$
4. What are the two types of memory locations that a programmer can reserve?

> The answers to the Mini-Quiz questions are located in Appendix A.

# # Selecting a Data Type for a Memory Location

Like storage bins, memory locations come in different types and sizes. The type and size you use depends on the item you want the memory location to store. Some memory locations can store a number, while others can hold text, a date, or a Boolean value (true or false). The item that a memory location will accept for storage is determined by the location's data type, which the programmer assigns to the location when he she declares it in a program. The most commonly used types in C++ are listed in Figure 3-5, along with the values each type can store and the amount of memory needed to store a value. Except for the string data type, the data types listed in the figure below to a