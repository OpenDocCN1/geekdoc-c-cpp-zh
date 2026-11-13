with heapsort, we can achieve quicksort's fast running time on almost all inputs, with heapsort's O(n log n) worst-case running time. Exercise 7.27 describes this approach.

The quicksort algorithm is simple to understand and prove correct, although for many years it had the reputation of being an algorithm that could in theory be highly optimized but in practice was impossible to code correctly. Like mergesort, quicksort is a divide-and-conquer recursive algorithm.

Let us begin with the following simple sorting algorithm to sort a list. Arbitrarily choose any item, and then form three groups: those smaller than the chosen item, those equal to the chosen item, and those larger than the chosen item. Recursively sort the first and third groups, and then concatenate the three groups. The result is guaranteed by the basic principles of recursion to be a sorted arrangement of the original list. A direct implementation of this algorithm is shown in Figure 7.13, and its performance is, generally speaking, quite

```
template <typename Comparable>
void SORT( vector<Comparable> & items )
{
if( items.size( ) > 1 )
{
vector<Comparable> smaller;
vector<Comparable> same;
vector<Comparable> larger;

auto chosenItem = items[ items.size( ) / 2 ];

for( auto & i : items )
{
if( i < chosenItem )
smaller.push_back( std::move( i ) );
else if( chosenItem < i )
larger.push_back( std::move( i ) );
else
same.push_back( std::move( i ) );
}

SORT( smaller ); // Recursive call!
SORT( larger ); // Recursive call!

std::move( begin( smaller ), end( smaller ), begin( items ) );
std::move( begin( same ), end( same ), begin( items ) + smaller.size( ) );
std::move( begin( larger ), end( larger ), end( items ) - larger.size( ) );
}
}
```

# Figure 7.13 Simple recursive sorting algorithm