```
#include<iostream>
#include<fstream>
using namespace std;
int main()
{
 fstream fio;
 fio.open("a.doc",ios::out);
 if(!fio.is_open())
 {
 cout<<("Can't open the file");
 return -1;
 }
 fio<<"Hacking: Exploiting computer security with Aman";
 fio.close();
 fio.open("a.doc",ios::in);
 char ch;
 do
 {
 ch=fio.get();
 cout<<ch;
 }while(!fio.eof());
 fio.close();
 return 0;
}
```

# Output

Hacking: Exploiting computer security with Aman