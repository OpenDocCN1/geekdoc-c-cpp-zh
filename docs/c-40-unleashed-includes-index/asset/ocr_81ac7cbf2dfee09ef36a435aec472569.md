Unless specified otherwise, ordering is based, as you will see, on the default IComparer for the element type, as obtained through IComparer<T>.Default. We discuss the concept of comparers in Chapter 16, “Collection Types.”

# SLIGHTLY MORE EAGER

To establish an ordering, all elements from the source sequence need to be known before any element from the ordered sequence can be returned. Although the use of an ordering in a query expression still keeps the entire query lazy, the effect of requesting the first element from the resulting sequence is quite an eager operation because it “drains” the whole source sequence to establish the ordering.

Compare this to Where and Select, which just take enough elements out of the source to produce one result sequence element at a time. For Select, this is a one-to-one relationship: asking the next element from the result causes Select to fetch the next element from the source and apply the projection function. Where is a bit greedier at times because it needs to consume elements from the source until the filter function evaluates true.

OrderBy can't do anything but load all the elements in the source to perform a sort on all of them. Notice we're only talking about LINQ to Objects here, where this causes all source elements to end up in an in-memory collection suitable for performing sorting operations on. In case of remote LINQ execution (for example, using LINQ to SQL), the ordering operation will be remoted to the server and execute there.

# Nontrivial Orderings

As you can already guess by now, the orderby clause simply expects a valued expression that produces the key value to order by. Any expression will do, from the absurd to the useful:

```
// Not incredibly useful but constants are expressions. Notice this doesn't
// guarantee to return the products in the input order!
var orderByConstant = from product in products
    orderby 1
    select product;

// Expensive to cheap requires descending sort.
var decreasingPrice = from product in products
    orderby product.Price descending
    select product;

// Calling a method and using a closure over a captured local variable.
DateTime from = DateTime.Now - TimeSpan.FromDays(100);
var topSellers = from p in products
    orderby p.GetNumberOfSalesSince(from) descending
    select p;
```