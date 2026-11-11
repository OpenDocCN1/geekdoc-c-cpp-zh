```
```cpp
cout<<"Enter the ID,name and tel_no of first customer"<<endl;
c1.input();
cout<<"Enter the ID, name and tel_no of second customer"<<endl;
c2.input();
cout<<"**********C1 calls issue**********"<<endl;
c1.issue();
cout<<"*********C1 calls issue**********"<<endl;
c1.issue();
cout<<"*******C1 returns a book**********"<<endl;
c1.return_book();
cout<<"*********C2 calls issue**********"<<endl;
c2.issue();
cout<<"********Customer C1********"<<endl;
c1.output();
cout<<"********Customer C2********"<<endl;
c2.output();
}
```
```

# EXERCISE

Trace the output of this program assuming input data of your choice.

# SCRATCH PAD

+   - As we need to store the data about books and customers in a library we create the following two classes so as to solve a given problem statement.
+     1. Book
+     2. Customer

**Book:** The class Book defines the data elements that are to be stored for each book in a real world. Hence, we create members of class Book as `book_id`, `title`, `author`. The class also defines the member functions `input()` and `output()` so as to read and print the details of each Book object.

**Customer:** Each object of class Customer represents one customer of the library in a real world. Hence, we define members `customer_id`, `name` and `tel_no` inside class Customer so as to store the relevant information about each customer in the computer memory. Further, it is a rule that each customer can at the most issue two books at a time. Hence, we create an array of class Book inside class Customer so as to represent the data about books that are issued by the customer.

```
```cpp
Book b[2];
```
```

However, not every customer will always issue 2 books from the library. Hence we have also created a variable `books_issued` which represents the count of number of books issued by a particular customer. We invoke a function `issue()` if the customer wants to issue a book from the library and we invoke a function `return_book()`.