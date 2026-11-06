A destructor refers to a special member function of a class that is run anytime an object of the class goes out of scope. A destructor takes the same name as a class but it should be preceded by a tilde (~). A destructor cannot take parameters neither can it return a value.

A destructor is a useful tool for releasing the memory resources before leaving a program. You can overload or inherit a destructor. The following example demonstrates how to use a destructor:

```
```csharp
using System;

namespace ConstructorApplication {
    class Person {
        private double height;  // Height of a person

        public Person() {  // A constructor
            Console.WriteLine("We are creating an object");
        }

        ~Person() {  //A destructor
            Console.WriteLine("We are deleting an object");
        }

        public void setHeight( double heig ) {
            height = heig;
        }

        public double getHeight() {
            return height;
        }

        static void Main(string[] args) {
            Person p = new Person();

            // set the height of the person
            p.setHeight(7.0);

            Console.WriteLine("The height of the person is : {0}",
```
```