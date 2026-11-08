
```cpp
}
else
{
    cout << "Unknown SAMPLE : " << name << endl;
}
}

void soldItemsList(multimap<string, SAMPLE*>& inventory, multiset <int> &soldItems)
{
    multimap<string, SAMPLE*>::iterator it = inventory.begin();
    for(it = inventory.begin(); it != inventory.end(); ++it)
    {
        int soldCount = soldItems.count((*it->second).sampleItem_Code_);
        cout<<"SAMPLE = " << (*it->second).name_ << ", Amount Sold = "
            << soldCount << endl;
    }
}

int checkSales(multimap<string, SAMPLE*>& inventory, multiset <int> &soldItems)
{
    int totalSales = 0;
    multimap<string, SAMPLE*>::iterator it;
    for(it = inventory.begin(); it != inventory.end(); ++it)
    {
        int soldCount = soldItems.count((*it->second).sampleItem_Code_);
        totalSales += soldCount * (*it->second).price_;
    }
    return totalSales;
}

int main()
{
    multimap<string, SAMPLE*> inventory;
    SAMPLE* prod1 = new SAMPLE("sample1", 2334, 10);
    SAMPLE* prod2 = new SAMPLE("sample2", 4556, 50);
    inventory.insert(pair<string, SAMPLE*>("sample1", prod1));
    inventory.insert(pair<string, SAMPLE*>("sample2", prod2));

    multiset <int> soldItems;

    sellSAMPLE("sample1", inventory, soldItems);
    sellSAMPLE("sample2", inventory, soldItems);
    sellSAMPLE("SHIRT", inventory, soldItems);
    sellSAMPLE("sample1", inventory, soldItems);
    sellSAMPLE("sample1", inventory, soldItems);
    sellSAMPLE("sample2", inventory, soldItems);

    soldItemsList(inventory, soldItems);

    cout<<"Total Amount of Sample Sold = " << checkSales(inventory, soldItems) << endl;

    delete prod1;
    delete prod2;
    return 0;
}
```

前面程序的输出如下：

![](img/43c5f409f9b17790a628c4b4df854b61_950_0.png)

- 4. 实现一个 C++ 程序，在类内部实例化 multimap。

```cpp
#include<iostream>
#include<map>
#include <string>

using namespace std;

class mapInstantiator
{
public:
    ~mapInstantiator();
    void createMultiMap(void);
    void insertElements(pair<string, int> element);
    void printer(void);
private:
    multimap<string, int> *phoneNums;
};

void mapInstantiator::createMultiMap(void)
{
    //Instantiate
    phoneNums = new multimap<string, int>;
}

void mapInstantiator::insertElements(pair<string, int> element)
{
    phoneNums->insert(element);
}

void mapInstantiator::printer(void)
{
    cout<<"\n\nMultimap printer method"<<endl;
    cout<<"Map size = "<<phoneNums->size()<<endl;
    multimap<string, int>::iterator it = phoneNums->begin();
    while(it != phoneNums->end())
    {
        cout<<"Key = "<<it->first<<"    Value = "<<it->second<<endl;
        it++;
    }
}

mapInstantiator::~mapInstantiator()
{
    //Don't forget to delete the pointer
    delete phoneNums;
}

int main()
{
    mapInstantiator aClass;
    aClass.createMultiMap();

    //Insert key, value as pairs
    aClass.insertElements(pair<string, int>("SUVANKAR",3839));
    aClass.insertElements(pair<string, int>("PRINON",8483));
    aClass.insertElements(pair<string, int>("ISHAN",8373));
    aClass.insertElements(pair<string, int>("SUVANKAR",8275));
    aClass.insertElements(pair<string, int>("PRINON",9287));
    aClass.insertElements(pair<string, int>("ISHAN",9463));

    aClass.printer();

    return 0;
}
```

前面程序的输出如下：

![](img/43c5f409f9b17790a628c4b4df854b61_951_0.png)

- 5. 实现一个 C++ 程序，示例说明 multimap 的用法。

```cpp
#include<iostream>
#include<map>
#include <string>

using namespace std;

//forward declaration
void printer(multimap<string, int> PR);

int main()
{
    multimap<string, int> TEL_NO;

    //Insert key, value as pairs
    TEL_NO.insert(pair<string, int>("SUVANKAR",9027));
    TEL_NO.insert(pair<string, int>("ISHAN",9836));
    printer(TEL_NO);

    //Insert duplicates
    TEL_NO.insert(pair<string, int>("SUVANKAR", 8938));
    TEL_NO.insert(pair<string, int>("PRINON",9835));
    TEL_NO.insert(pair<string, int>("SUVANKAR",7893));
    TEL_NO.insert(pair<string, int>("ISHAN",8928));
    printer(TEL_NO);

    //Checking frequency of different keys
    cout<<"\n\nFrequency of VARIOUS Names"<<endl;
    cout<<"Number of Phones for SUVANKAR = "<<TEL_NO.count("SUVANKAR")<<endl;
    cout<<"Number of Phones for ISHAN = "<<TEL_NO.count("ISHAN")<<endl;
    cout<<"Number of Phones for PRINON = "<<TEL_NO.count("PRINON")<<endl;
    cout<<"Number of Phones for JUMI = "<<TEL_NO.count("JUMI")<<endl;

    //Print all SUVANKAR from the list and then erase them
    pair<multimap<string,int>::iterator, multimap<string,int>::iterator> ii;
    multimap<string, int>::iterator it;   //Iterator to be used along with ii
    ii = TEL_NO.equal_range("SUVANKAR");  //We get the first and last entry in ii
    cout<<"\n\nPrinting all SUVANKAR and then deleting them"<<endl;
    for(it = ii.first; it != ii.second; ++it)
    {
        cout<<"Key = "<<it->first<<"    Value = "<<it->second<<endl;
    }
    TEL_NO.erase(ii.first, ii.second);
    printer(TEL_NO);
    return 0;
}

//This method prints the vector
void printer(multimap<string, int> PR)
{
    cout<<"\n\nMultimap printer method"<<endl;
    cout<<"Map size = "<<PR.size()<<endl;
    multimap<string, int>::iterator it = PR.begin();
    while(it != PR.end())
    {
        cout<<"Key = "<<it->first<<"    Value = "<<it->second<<endl;
        it++;
    }
}
```

## 第 B 章

前面程序的输出如下：

![](img/43c5f409f9b17790a628c4b4df854b61_953_0.png)

- 6. 实现一个 C++ 程序，在不使用第三个变量的情况下，用一行代码交换两个变量。

```cpp
#include<iostream>
using namespace std;

void PROCESS_1(int& x, int& y)
{
    cout<<"\nPROCESS_1"<<endl;
    x^=y^=x^=y;
}

void PROCESS_2(int& x, int& y)
{
    cout<<"\nPROCESS_2"<<endl;
    x = ((x = x + y) - (y = x - y));
}

void PROCESS_3(int& x, int& y)
{
    cout<<"\nPROCESS_3"<<endl;
    x = ((x = x * y) / (y = x / y));
}

int main()
{
    int x = 4, y = 5;
    cout << "\nOriginal" << endl;
    cout << "x = " << x << ", y = " << y << endl;
    PROCESS_1(x, y);
    cout << "x = " << x << ", y = " << y << endl;

    x = 4, y = 5;
    PROCESS_2(x, y);
    cout << "x = " << x << ", y = " << y << endl;

    x = 4, y = 5;
    PROCESS_3(x, y);
    cout << "x = " << x << ", y = " << y << endl;

    return 0;
}
```

前面程序的输出如下：

![](img/43c5f409f9b17790a628c4b4df854b61_954_0.png)

请注意，前面的程序仅适用于整数。

- 7. 使用 C++ 实现 isNumeric() 函数。

```cpp
#include <string>
#include <sstream>
using namespace std;

bool isNumeric1(string stringToCheck)
{
    bool numeric = false;
    if(stringToCheck.find_first_not_of("0123456789.") == string::npos)
        numeric = true;
    return numeric;
}

bool isNumeric2(string stringToCheck)
{
    bool numeric = true;
    unsigned i = 0;
    while(numeric && i < stringToCheck.length())
    {
        switch (stringToCheck[i])
        {
            case '0': case '1': case '2': case '3': case '4': case '5': case '6':
            case '7': case '8': case '9': case '.':
                //do nothing
                break;
            default:
                numeric = false;
        }
        i++;
    }
    return numeric;
}

bool isNumeric3(string stringToCheck)
{
    stringstream streamVal(stringToCheck);
    double tempVal;
    streamVal >> tempVal;

    if(streamVal.get() != EOF)
        return false;
    else
        return true;
}

int main()
{
    string str1("45345"), str2("6534.985"), str3("DFK154542AB");
    cout << "\nPROCESS_1" << endl; cout << str1 << (isNumeric1(str1) ? " is Numeric" : " is Not Numeric") << endl;
    cout << str2 << (isNumeric1(str2) ? " is Numeric" : " is Not Numeric") << endl;
    cout << str3 << (isNumeric1(str3) ? " is Numeric" : " is Not Numeric") << endl;

    cout << "\nPROCESS_2" << endl; cout << str1 << (isNumeric2(str1) ? " is Numeric" : " is Not Numeric") << endl;
    cout << str2 << (isNumeric2(str2) ? " is Numeric" : " is Not Numeric") << endl;
    cout << str3 << (isNumeric2(str3) ? " is Numeric" : " is Not Numeric") << endl;

    cout << "\nPROCESS_3" << endl; cout << str1 << (isNumeric3(str1) ? " is Numeric" : " is Not Numeric") << endl;
    cout << str2 << (isNumeric3(str2) ? " is Numeric" : " is Not Numeric") << endl;
    cout << str3 << (isNumeric3(str3) ? " is Numeric" : " is Not Numeric") << endl;
    system("pause");
    return 0;
}
```
