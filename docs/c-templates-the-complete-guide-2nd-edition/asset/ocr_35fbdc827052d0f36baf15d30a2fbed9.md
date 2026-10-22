values: Click here to view code image

# inherit/person.hpp

```
struct Person {
std::string firstName;
std::string lastName;

friend std::ostream& operator<<(std::ostream& strm, Person const& p) {
return strm << p.lastName << ", " << p.firstName;
}
};
```

However, rather than iterating over all of the Person values in the container, we only want to see the first names. In this section, we develop an iterator adapter called ProjectionIterator that allows us “project” the values of an underlying (base) iterator to some pointer-to-data member, for example, Person::firstName.

A ProjectionIterator is an iterator defined in terms of the base iterator (Iterator) and the type of value that will be exposed by the iterator (T): Click here to view code image

# inherit/projectioniteratorskel.hpp

```
template<typename Iterator, typename T>
class ProjectionIterator
: public IteratorFacade<
ProjectionIterator<Iterator, T>,
T,
typename std::iterator_traits<Iterator>::iterator_category,
T&,
typename std::iterator_traits<Iterator>::difference_type>
{
using Base = typename std::iterator_traits<Iterator>::value_type;
using Distance =
typename std::iterator_traits<Iterator>::difference_type;

Iterator iter;
T Base::* member;

friend class IteratorFacadeAccess
... //implement core iterator operations for IteratorFacade
public:
ProjectionIterator(Iterator iter, T Base::* member)
: iter(iter), member(member) { }
};

template<typename Iterator, typename Base, typename T>
```