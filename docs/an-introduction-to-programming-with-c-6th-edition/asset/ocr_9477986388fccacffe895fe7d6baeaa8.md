# CHAPTER 11 One-Dimensional Arrays

| //Modified XYZ Company.cpp - displays the contents |
| //of an array |
| //Created/revised by <your name> on current date> |
| #include <iostream> |
| #include <iomanip> the name |
| using namespace std; | optional |
| //function prototype |
| void displayArray(double dollars[], int numElements); | function prototype |
| int main() {
| //declare array
| double sales[4] = {0.0};
| //fill array with data
| for (int sub = 0; sub < 4; sub += 1) {
| cout << "Enter the sales for Region ";
| cin >> sub[sub];
} //for for
| //display the contents of the array
| displayArray(sales, 4); | function call |
| system("pause"); | your C++ development tool may
| not require this statement |
| return 0;
} //end of main function | function header |
| ***function definitions****
| void displayArray(double dollars[], int numElements) {
| cout << fixed << setprecision(2) << endl;
| for (int sub = 0; sub < numElements; sub += 1) {
| cout << "Sales for Region " << sub + 1 << ": $\$";
| cout << dollars[sub] << endl;
} //for for
} //end of displayArray function |

Figure 11-19 XYZ Company's modified samples program

Figure 11-20 shows the completed desk-check for the XYZ Company's modified sales program. Recall from Chapter 10 that you pass a variable by reference to a function, the computer locates the variable and assigns the name of the corresponding formal parameter to the variable. The same process occurs with array variables and explains why each variable in Figure 11-20 has two names: one assigned by the main function, and the other by the displayArray function. Both functions access the memory locations where array variables reside, each uses a different name to do so. The main function uses the name sales, whereas the displayArray function uses the name dollars.