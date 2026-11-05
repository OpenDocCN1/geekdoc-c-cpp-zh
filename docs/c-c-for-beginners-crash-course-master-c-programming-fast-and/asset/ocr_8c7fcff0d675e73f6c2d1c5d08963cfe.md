# 13.1 Introduction to Operator Overloading

The built in operators can be redefined or overloaded in C#. The overloaded operators are functions having an **operator** keyword. It is followed by the symbol for the operator to be defined. The overloaded operator has a return type and a parameter list.

**Example:**

```
```csharp
// Example 50:
using System;
namespace operator1
{
    class Room
    {
        private int length;
        private int breadth;

        public int getArea()
        {
            return length * breadth;
        }

        public void setlen (int len)
        {
            length = len;
        }

        public void setbread (int bread)
        {
            breadth = bread;
        }

        //+ operator is overloaded
        public static Room operator + (Room r, Room s)
        {
            Room o = new Room();
            o.length = r.length + s.length;
            o.breadth = r.bread + s.bread;
            return o;
        }
    }

    class Program
    {
        public static void Main(string[] args)
        {
            Room o1 = new Room();
```
```