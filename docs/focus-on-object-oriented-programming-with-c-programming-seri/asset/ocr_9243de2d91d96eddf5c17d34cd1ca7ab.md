# Overloading Unary Operators

Let's start off by overloading a unary operator. Unary operators act on only one operand (++, --, -).

We'll look at the Counter class we previously defined. Objects of that class were incremented by calling a member function:

```
c1.incCount();
```

That did the job, but the listing would have been more readable if we could have used the increment operator ++ and simply said:

```
++c1;
```

Here's our newest version of the Counter class, rewritten to use an overloaded increment variable:

```
class Counter {
   private:
      int count;
   public:
      Counter() { count = 0; }
      int getCount() { return count; }
      void operator++() { ++count; }
};

int main() {
   Counter c1, c2;
   cout << "c1 = " << c1.getCount() << endl;
   cout << "c2 = " << c2.getCount() << endl;
   ++c1;
   ++c2;
   cout << "c1 = " << c1.getCount() << endl;
   cout << "c2 = " << c2.getCount() << endl;
   return 0;
}
```