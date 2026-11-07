**16.8**  *(Modules: Imports Are Not Transitive)* Explain what it means when we say that “import statements are not transitive.”

# Modules Code Exercises

**16.9**  *(Modules: Importing Standard Library Headers as Header Units)* The program in Fig. 14.1 `#includes` several standard library headers. Modify Fig. 14.1 to replace each header’s `#include` with a corresponding `import` statement. Compile and run the program to confirm that it produces the same results shown in Fig. 14.1.

**16.10**  *(Modules: Creating a Module)* The program in Fig. 5.10 defined overloaded square functions. Refactor that program’s code as follows:

+   - Create a module named `deitel.squares` containing the two square overloads.
+   - In the module, place the functions in the namespace `deitel::squares` and export the namespace’s contents.
+   - Create a separate `.cpp` file for the main function. In this file, import the module and modify your code to use the versions of the overloaded functions from the `deitel::squares` namespace.

Compile the program and run it to confirm that it produces the same results shown in Fig. 5.10.

**16.11**  *(Modules: Creating a Module)* Modify your module from Exercise 16.10 so that rather than exporting the entire `deitel::squares` namespace, it exports only the square function that receives an `int` parameter. Does the main application still compile? If so, when you run it, does it produce the same output as in Fig. 5.10?

**16.12**  *(Modules: Separating Interface from Implementation)* Section 9.22 defined a custom Cipher class that implemented the Vigenère secret-key cipher algorithm. Refactor that example:

+   - Create a module named `deitel.encryption` containing the Cipher class’s definition.
+   - In the module, separate the Cipher class’s interface from its implementation, as demonstrated in Section 16.8.2.
+   - Place the class in namespace `deitel::encryption` and export the namespace.
+   - In the main application’s `.cpp` file, import the `deitel.encryption` module, and qualify class Cipher’s name with the `deitel::encryption` namespace.

Compile the program and run it to confirm that it produces the same results shown in Section 9.22.

**16.13**  *(Modules: private Module Fragment)* Modify your solution to Exercise 16.12 to define the entire class in the primary module interface unit.

**16.14**  *(Modules: Partitions)* Using the techniques shown in Section 16.9.1, modify your solution to Exercise 16.10 to define each square function in a separate partition.

**16.15**  *(Modules: Reduced Translation Unit Sizes)* The program in Fig. 14.1 `#includes` several standard library headers. For your compiler, use the techniques we discussed in Section 16.5 to preprocess Fig. 14.1 and determine its translation unit size in bytes. Then,