In this case, the exception you would care about is a predefined exception called failbit: If the file does not open correctly, then a failbit exception is thrown. So, for this code, because the fstream is named infile, the command you'll write is infile.exceptions(fstream::failbit) (9).

Then, you have a try block (d), where the code you want to try to run is put inside the curly braces. In this case, the code you're trying is opening the file.

Following that is a catch block (e), which takes in one parameter—a reference to an exception, given the name category in this case.

Inside the catch block is the code you want to run if the exception is caught. In this case, you print out a message that there was an error opening the file. Then, you return a nonzero value. Because you're in the main function, return means that the program ends, and because it ended with a nonzero value, it indicates that there was an error along the way.

If you run this code and the file does not exist, then the open function you tried to call will generate an exception. And when this exception is caught, you print out Error opening file, and the program ends.

If there was not an exception, then you would have just skipped over the catch block and gone on to the remaining code in the main function.

```
// Program 14_6
// Exception example - reading a nonexistent file, now with try/catch
#include <iostream>
#include <fstream>
using namespace std;

int main() {
    fstream infile;
    infile.exceptions(fstream::failbit);
    try {
        infile.open("something.dat", fstream::in);
    }
    catch (exception& category) {
        cout << "Error opening file" << endl;
        return 1;
    }
    int a;
    infile >> a;
    cout << "Read in: " << a << endl;
}
```