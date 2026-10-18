# DISPLAY 8.3 Robust Input Function (part 2 of 2)

```
13  int main()
14  {
15      using namespace std;
16      int inputNumber;
17      getInt(inputNumber);
18      cout << "Final value read in = " <<inputNumber<<endl;
19      return 0;
20  }
```

```
21  //Uses iostream and readAndClean:
22  void getInt(int& inputNumber)
23  {
24      using namespace std;
25      char ans;
26      do
27      {
28          cout << "Enter input number: ";
29          readAndClean(inputNumber);
30          cout << "You entered " <<inputNumber
31              << " Is that correct? (yes/no): ";
32          cin >> ans;
33          newLine();
34      } while ((ans != 'y') && (ans != 'Y'));
35  }
```

```
36  //Uses iostream, cstdlib, and cctype:
37  void readAndClean(int& n)
```

<The rest of the definition of readAndClean is given in Display 8.2.>

```
38  //Uses iostream:
39  void newLine()
```

<The rest of the definition of newLine is given in Display 8.2.>

# Sample Dialogue

```
Enter input number: $57
You entered 57 Is that correct? (yes/no): no
Enter input number: $77*5xa
You entered 775 Is that correct? (yes/no): no
Enter input number: 77
You entered 77 Is that correct? (yes/no): no
Enter input number: $75
You entered 75 Is that correct? (yes/no): yes
Final value read in = 75
```