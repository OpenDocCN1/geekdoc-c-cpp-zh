# 10.9.2 Creating and Accessing Dense Vectors

We first create a number of dense vectors based on the options in Figure 10.1. We can create vectors having both numeric and non-numeric underlying data types and given storage arrays. Note that we use an alias for the Boost uBLAS namespace:

```
#include <boost/numeric/ublas/vector.hpp>      // The vector class.
#include <boost/numeric/ublas/io.hpp>              // Sending to IO stream.

namespace ublas=boost::numeric::ublas;

ublas::vector<double> v1(10);
ublas::vector<double, ublas::unbounded_array<double> > v2(10);
ublas::vector<double, ublas::bounded_array<double, 20> > v3(10);
ublas::vector<double> v4(5, 3.14);
ublas::vector<double, vector<double> > v5(10, 4.5);
cout<<"v5: "<<v5<<endl;

ublas::vector<char, vector<char> > v6(10, 'd');
cout<<"v6: "<<v6<<endl;
```

We can access and modify the elements of a vector using overloaded operators:

```
// Fill the vectors.
for (int i=0; i<10; i++)
{
    // Use the [] operator.
    v1[i]=i;

    // Use the () operator.
    v2(i)=i+10;
    v3(i)=i+20;
}
```

We now show the use of composite operators and the support for iterators:

```
// Operators.
// When adding/subtracting two vectors, they should have the same size.
cout<<endl<<"*** Operators ***"<<endl;
cout<<"v1+=v3:  "<<(v1+=v3)<<endl;
cout<<"v1-=v3:  "<<(v1-=v3)<<endl;
cout<<"v1*=2.5: "<<(v1*=2.5)<<endl;
cout<<"v1/=2.5: "<<(v1/=2.5)<<endl;

// Iterators.
cout<<endl<<"*** Iterators ***"<<endl;
transform(v1.begin(), v1.end(), v2.begin(), v3.begin(),
          multiplies<double>());
cout<<"Multiply v1 & v2 to v3 using transform algorithm ";
cout<<"and multiplies function object: "<<v3<<endl;
```