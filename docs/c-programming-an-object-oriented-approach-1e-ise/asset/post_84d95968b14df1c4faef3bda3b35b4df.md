
![](img/d68f6199646ca63591a6d8419e0ed4ba_547_0.png)

**Figure 11.22** Sequence diagram for the *First* and *Second* classes

![](img/d68f6199646ca63591a6d8419e0ed4ba_547_1.png)

**Figure 11.23** UML class diagram for *Invoice* and *Product* classes

We show the sequence diagram for two products in Figure 11.24. Note that the *main* function must instantiate two objects of type *Product* and one object of type *Invoice*. The *main* function then calls the *add* function in the *Invoice* class to add the products to the invoice, but it must get the price of each product from the corresponding object.

![](img/d68f6199646ca63591a6d8419e0ed4ba_547_2.png)

**Figure 11.24** Sequence diagram for the *Invoice* program

**Program 11.24** File product.h

```cpp
/**************************************************************
 * The interface file for the Product class                    *
 ***************************************************************/
#ifndef PRODUCT_H
#define PRODUCT_H
#include <string>
#include <iostream>
using namespace std;

class Product
{
    private:
        string name;
        double unitPrice;
    public:
        Product (string name, double unitPrice);
        ~Product ();
        double getPrice ( ) const;
};
#endif
```

**Product Class.** Program 11.24 is the interface for the *Product* class.  
Program 11.25 is the implementation file for the *Product* class.

**Program 11.25** File product.cpp

```cpp
/**************************************************************
 * The implementation file for Product class                  *
 ***************************************************************/
#include "product.h"

// Constructor
Product :: Product (string nm, double up)
: name (nm), unitPrice (up)
{
}
// Destructor
Product :: ~Product ( )
{
}
// The getPrice member function
double Product :: getPrice ( ) const
{
    return unitPrice;
}
```

**Program 11.26** File `invoice.h`

```cpp
/**************************************************************
 * The interface file for the Invoice class                    *
 **************************************************************/
#ifndef INVOICE_H
#define INVOICE_H
#include "product.h"

class Invoice
{
private:
   int invoiceNumber;
   double invoiceTotal;
public:
   Invoice (int invoiceNumber);
   ~Invoice ( );
   void add (int quantity, Product product);
   void print ( ) const;
};
#endif
```

**Invoice Class.** Program 11.26 is the interface file for the *Invoice* class. Program 11.27 shows the implementation file for the *Invoice* class.

**Program 11.27** File `invoice.cpp`

```cpp
/**************************************************************
 * The implementation file for Invoice class                   *
 **************************************************************/
#include "invoice.h"

// Constructor
Invoice::Invoice (int invNum)
: invoiceNumber (invNum), invoiceTotal (0.0)
{
}
// Destructor
Invoice::~Invoice ( )
{
}
// Add member function
void Invoice::add (int quantity, Product product)
{
   invoiceTotal += quantity * product.getPrice ( );
}
// Print member function
void Invoice::print() const
{
    cout << "Invoice Number: " << invoiceNumber << endl;
    cout << "Invoice Total: " << invoiceTotal << endl;
}
```

**Application** Program 11.28 is the application file for testing the *Invoice* class.

**Program 11.28** File `application.cpp`

```cpp
/********************************************************************
 * The application file to test the Invoice class                    *
 ********************************************************************/
#include "invoice.h"

int main()
{
    // Instantiation of two products
    Product product1("Table", 150.00);
    Product product2("Chair", 80.00);
    // Creation of invoice for the two products
    Invoice invoice (1001);
    invoice.add (1, product1);
    invoice.add (6, product2);
    invoice.print();
    return 0;
}
```

```text
Run:
Invoice Number: 1001
Invoice Total: 630
```

## 11.4 PROGRAM DESIGN

In this section we discuss two projects. The first shows how to create a *Tokenizer* class; the second shows how to simulate the registration process at a university.

### 11.4.1 A Tokenizer Class

A common problem is to tokenize a string of characters using a list of delimiters. For example, we may need to extract words from a text. The words in a text are separated by spaces and new-line characters. The words in this case are called *tokens*, and the characters that separate the words are *delimiters*. For example, the following string has seven tokens (words) in it.

> "This is a book about C++ language"

![](img/d68f6199646ca63591a6d8419e0ed4ba_551_0.png)

**Figure 11.25** Relationship between classes

The C++ language has no class whose objects can tokenize a string, but we can create a class to do so. The string library class has member functions that search a string to find a character in a string or to find a character which is not in a string. We can use these functions in the string library to create a *Tokenizer* class.

**Relationship Among Classes**

Before writing the code for the *Tokenizer* class, we show the UML class diagram that depicts the relationship between classes. We use only two classes in this task: *Tokenizer* class and *string* class. Figure 11.25 shows the relationship between these two classes.

In Figure 11.25 the *Tokenizer* class uses the *string* class three times. It uses it to create the target string (the text to be tokenized), to create the delimiter string, and finally to create tokens. We have one string as a target and one string as a delimiter, but we create many strings as tokens. The relationship between the tokenizer object and the target or delimiter object is composition. The relationship between the tokenizer object and tokens is dependency (the tokens are returned objects from functions in the *Tokenizer* class).

**Sequence Diagram**

Figure 11.26 shows the interaction between objects in a sequence diagram.

![](img/d68f6199646ca63591a6d8419e0ed4ba_551_1.png)

**Figure 11.26** Sequence diagram for the *Tokenizer* design

**Program 11.30** File tokenizer.cpp

```cpp
1 /************************************************************
2  * The implementation file for the Tokenizer class
3  ************************************************************/
4 #include "tokenizer.h"
5
6 // Constructor
7 Tokenizer :: Tokenizer (const string& tar, const string& del)
8 : target (tar), delim (del)
9 {
10    begin = target.find_first_not_of (delim, 0);
11    end = target.find_first_of (delim, begin);
12 }
13 // Destructor
14 Tokenizer :: ~Tokenizer()
15 {
16 }
17 // Checks for more tokens
18 bool Tokenizer :: moreToken () const
19 {
20    return (begin != -1);
21 }
22 // Returns the next token
23 string Tokenizer :: nextToken ()
24 {
25    string token = target.substr (begin, end - begin);
26    begin = target.find_first_not_of (delim, end);
27    end = target.find_first_of (delim, begin);
28    return token;
29 }
```

**Program 11.31** File app.cpp

```cpp
1 /************************************************************
2  * The application file to test the Tokenizer class
3  ************************************************************/
4 #include "tokenizer.h"
5
6 int main ()
7 {
8    // The target string that needs to be tokenized
9    string target ("This is the string to be tokenized. \n");
10   // The delimiter string defines the set of separators
11   string delimit (" \n");  // Delimiter made of ' ' and '\n'
12   // Instantiation of tokenizer object
13   Tokenizer tokenizer (target, delimit);
14   // Traversing the target string to find tokens
15   while (tokenizer.moreToken())
16   {
17       cout << tokenizer.nextToken() << endl;
18   }
19   return 0;
20 }
```

```text
Run:
This
is
the
string
to
be
tokenized.
```

### 11.4.2 Registration

In this section we use association and dependency between classes to design a simple registration system for a small department in a college or university.

**UML Class Diagram**

We use six classes as shown in Figure 11.27.

Each *student* object composes a *string* object (as student name) and composes a *schedule* object, which in turn composes an array of student names (strings). Each *course* object composes a *string* object (as course name) and composes a *roster* object, which in turn composes an array of course names (strings). The registrar class just uses the *student* and *course* objects.

**UML Sequence Diagram**

Before writing the code for the five user-defined classes involved, we show the sequence diagram and the interaction between the classes (Figure 11.28). Note that the *roster* object

![](img/d68f6199646ca63591a6d8419e0ed4ba_554_0.png)

**Figure 11.27** Relationship among classes in registration project
