# Is-a and Has-a Relationships

As mentioned earlier, public inheritance models get better in the program design an is-a relationship, that is, a derived class should also be a base class object. For example, the Book object is also a Product object. The Book class inherits the members of the Product class and add extra members that apply particularly to books and not to products in general, such as the author.

To understand the is-a relationship, I'll give you an example that does not match that. Suppose that we have a Bookstore class. A bookstore is not a book. Therefore, it'd be better to not derive the Book class from the Bookstore class. To clarify, if you make that derivation, it does not mean the code will compile or an error will occur when the program is executed. Nothing prevents you from doing that, but such a program design usually leads to programming problems. Since bookstore has books, the proper approach to associate classes is the model of the has-a relationship. That is, to include a Book object as a member of the Bookstore class.

I'll give you some examples. Suppose that you have defined the Engine class, the Tires class and you want to define the Car class. Since a car has an engine and tires, it'd fit to use the has-a model and writing something like that:

```
class Car
{
    Engine eng;
    Tires tir;
}
```

In another example of has-a relationship, suppose that you have defined the Date class and want to define the Employee class. Since an employee has date information we'd write:

```
class Employee
{
    Date hire_date;
    Date birth_date;
}
```

Now, suppose that you've defined the Shape class and want to define the Circle class. Since a circle is a shape, it'd fit to use the is-a model and writing something like that:

```
class Circle : public Shape
{\}
```

Similarly, suppose that you've defined the Account class and want to define the CheckingAccount class. Since checking an account is a special type of bank account we'd use inheritance.
What about an Animal class and a Cat class? Since a cat is a kind of animal, it is possible to use inheritance and derive Cat from Animal.

So, when you have decide whether to add a class as a member or derive from it, the general rule is to see which one of the has-a and is-a fits better and act accordingly.

# Protected Members and Inheritance

In general, when we create a class that might be used as a base class and want to allow access to some of its members from a derived class, we can declare those members protected instead of private. The protected