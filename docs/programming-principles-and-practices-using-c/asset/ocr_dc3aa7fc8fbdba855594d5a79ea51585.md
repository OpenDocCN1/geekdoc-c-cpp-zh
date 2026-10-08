This will now work for all kinds of sequences of shapes. In particular, we can even call it for the elements of an array of **Shapes**:

```
```
Point p {0,100};
Point p2 {50,50};
Shape* a[] = { new Circle{p,50}, new Triangle{p,p2,Point{25,25}} };
draw_all(a,a+2);
```
```

We could also provide a version that is simpler to use by restricting it to work on containers:

```
```
template<class Cont> void draw_all(Cont& c)
{
    for (auto& p : c) p->draw();
}
```
```

Or even, using C++14 concepts (§19.3.3):

```
```
void draw_all(Container& c)
{
    for (auto& p : c) p->draw();
}
```
```

The point is still that this code is clearly object-oriented, generic, and very like ordinary procedural code. It relies on data abstraction in its class hierarchy and the implementation of the individual containers. For lack of a better term, programming using the most appropriate mix of styles has been called *multi-paradigm programming*. However, I have come to think of this as simply *programming*; the “paradigms” primarily reflect a restricted view of how problems can be solved and weaknesses in the programming languages we use to express our solutions. I predict a bright future for programming with significant improvements in technique, programming languages, and support tools.

# ## 22.2 Programming language history overview

In the very beginning, programmers chiseled the zeros and ones into stones by hand! Well, almost. Here, we’ll start (almost) from the beginning and quickly introduce some of the major developments in the history of programming languages as they relate to programming using C++.

There are a lot of programming languages. The rate of language invention is at least 2000 a decade, and the rate of “language death” is about the same. Here, we cover almost 60 years by briefly mentioning ten languages. For more information, see [http://research.ihost.com/hopl/HOPL.html](http://research.ihost.com/hopl/HOPL.html). There, you can find links to all the articles of the three ACM SIGPLAN HOPL (History of Programming Languages) conferences. These are extensively peer-reviewed papers – and