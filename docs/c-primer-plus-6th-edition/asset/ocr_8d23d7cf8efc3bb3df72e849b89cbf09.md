hand, the nonmember version will allow you swap contents between two different kinds of containers.

Let's examine three representative STL functions: for_each(), random_shuffle(), and sort().The for_each() function can be used with any container class. It takes three arguments. The first two are iterators that define a range in the container, and the last is a pointer to function. (More generally, the last is function object; you'll learn about function shortly.) The for_each() function then applies the pointed-to-function must not alter the value of the container elements.You can use the for_each() function instead of a loop. For example, you can replace the code

```
vector<Review>::iterator pr;
for (pr = books.begin(); pr != books.end(); pr++)
ShowReview(*pr);
```

with the following:
for_each(books.begin(), books.end(), ShowReview);

This enables you to avoid tiring your hands (and code) with explicit use of iterator variables.
The random_shuffle() function takes two iterators that specify a range and rearranges the elements in that range random order. For example, the following statement rearranges the order of all the elements in the books vector:
random_shuffle(books.begin(), books.end());

Unlike for_each, which works with any container, this function requires that the container class allow random access, which the vector support.
The sort() function, too, requires that the container support random access. It comes in two versions. The first version takes two iterators to define a range, and it sorts the range by using the < operator defined for the type element stored in the container. For example, the following sorts the contents of coolstuff in ascending order, using the built-in < operator to compare values:

```
vector<int> coolstuff;
...
sort(coolstuff.begin(), coolstuff.end());
```

If the container elements are user-defined objects, then there has to be an operator() function defined with that type of object to use sort(). For example, you could sort a vector containing Review objects if you provided either a Review member function or a nonmember function for operator< (). Because Review is a structure, its members are public, like this:

```
bool operator<(const Review& r1, const Review& r2)
{
    if (r1.title < r2.title)
        return true;
```