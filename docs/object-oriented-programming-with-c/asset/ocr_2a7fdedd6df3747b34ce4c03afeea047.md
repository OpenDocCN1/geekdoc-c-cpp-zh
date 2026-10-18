```
```cpp
{
int iProductNumber;
string strProductName;
public:
Product()
{
}
Product(const int &number, const string &name)
{
setProductNumber(number);
setProductName(name);
}
void setProductNumber(int n)
{
iProductNumber = n;
}
void setProductName(const string str)
{
strProductName = str;
}
int getProductNumber()
{
return iProductNumber;
}
const string getProductName()
{
return strProductName ;
}
}
Products operator = (Product &source)
{
setProductNumber(source.iProductNumber);
string strTemp = source.strProductName;
setProductName(strTemp);
return *this;
}
void display()
{
}
```
```