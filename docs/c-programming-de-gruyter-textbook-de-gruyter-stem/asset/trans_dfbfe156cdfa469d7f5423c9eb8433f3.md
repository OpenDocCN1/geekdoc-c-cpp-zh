

## 4 类与对象

```cpp
//main函数
int main() {
    Point myp1(1,1),myp2(4,5); //创建 Point 类的对象
    Line line(myp1,myp2); //创建 Line 类的对象
    Line line2(line); //使用拷贝构造函数创建一个新对象

    cout<<"The length of the line is:";
    cout<<line.GetLen()<<endl;
    cout<<"The length of the line2 is:";
    cout<<line2.GetLen<<endl;
}
```

运行结果如下：

Point 的拷贝构造函数被调用
Point 的拷贝构造函数被调用
Point 的拷贝构造函数被调用
Point 的拷贝构造函数被调用
Line 的构造函数被调用
Point 的拷贝构造函数被调用
Point 的拷贝构造函数被调用
Line 的拷贝构造函数被调用
line 的长度为:
line2 的长度为:
