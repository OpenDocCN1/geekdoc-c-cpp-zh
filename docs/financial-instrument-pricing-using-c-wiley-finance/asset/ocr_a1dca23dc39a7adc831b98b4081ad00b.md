```
// Generate edge values
lattice1(j,0) = lattice1(j-1,0);
lattice1(j,lattice1.MaxIndex(j)) = lattice1(j-1,lattice1.MaxIndex(j-1));

// Generate the interior values
for (std::size_t i = 1; i < lattice1[j].size()-1; ++i)
{
    lattice1(j,i)=lattice1(j-1,i)+lattice1(j-1,i-1);
}
LatticeMechanisms::print(lattice1);
```

These examples show how to create a lattice and access and modify its values. You can run the code and examine the output.

We now create a generalised lattice whose row index set is a Boost date type. We first create a set of fixing dates that will form the row axis:

```
#include <boost/date_time/gregorian/gregorian.hpp>

// Dates as axis
namespace Dates = boost::gregorian;

// Simple dates for illustrative purposes
std::set<Dates::date> fixingDates;
Dates::date myDate(2014, Dates::May, 16);
fixingDates.insert(myDate);
Dates::date myDate2(2014, Dates::May, 26);
fixingDates.insert(myDate2);
Dates::date myDate3(2014, Dates::Jun, 2);
fixingDates.insert(myDate3);
Dates::date myDate4(2014, Dates::Jun, 12);
fixingDates.insert(myDate4);
```

We then create a generalised lattice based on these fixing dates:

```
GeneralisedLattice<Dates::date,double, 3> lattice2(fixingDates);
GeneralisedLatticeMechanisms::print(lattice2);
```

A useful project would be to extend the functionality to support dates.

# 11.4.3 Layer 2: Operations on Lattices

The functionality in Layer 1 is mainly concerned with generic classes that model lattice structures. In general, the focus lies on allocating memory for these structures and using operator overloading to access the elements of the lattices. This functionality is consistent with the SRP. These ADTs can be used in many kinds of applications (in this book we are mainly interested in option pricing). We develop code to iterate in lattices, use lattices