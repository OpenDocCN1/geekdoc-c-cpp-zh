```
```cpp
using namespace std;

int main(array<System::String ^> ^args)
{
    vector<int> numbers;
    srand(time(NULL));
    for(int i = 1; i <= 1000; ++i)
    {
        numbers.push_back(rand() % 100 + 1);
    }
    // display the numbers in the vector
    for(int i = 0; i < numbers.size(); ++i)
    {
        cout << numbers[i] << " ";
    }
    unsigned int sum = 0;
    for(int i = 0; i < numbers.size(); ++i)
    {
        sum += numbers[i];
    }
    cout << endl << endl << "The sum is: " << sum
         << endl;
    Console::ReadKey();
    return 0;
}
```
```

Using random numbers in this fashion is a major convenience. Very few people have the patience to enter 1000 values into a vector. Of course, another solution for finding data to test a program is to use a data file and read the data from the file into the vector. As so many textbook authors have said in the past, we'll leave that as an exercise for the reader.