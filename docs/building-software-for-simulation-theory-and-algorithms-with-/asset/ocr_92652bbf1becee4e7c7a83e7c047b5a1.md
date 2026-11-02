```
~~~cpp
  for (adevs::Bag<int>::iterator iter = xb.begin();
       iter != xb.end(); iter++)
    p += (*iter);
  }
  void delta_conf(const adevs::Bag<int>& xb)
  {
    delta_int();
    delta_ext(0.0,xb);
  }
  void output_func(adevs::Bag<int>& yb) { yb.insert(1); }
  double ta()
  {
    if (p > 0) return sigma;
    else return DBL_MAX;
  }
  void gc_output(adevs::Bag<int>&) {}
  double getSigma() const { return sigma; }
  int getParts() const { return p; }
private:
  const double tm; // Machining time
  int p; // Number of parts in the bin
  double sigma; // Time to the next output
};

#endif
~~~
```

# ### *Implementation of the Assembly-Line Model*

```
~~~cpp
#ifndef _AssemblyLine_h_
#define _AssemblyLine_h_
#include "Machine.h"

class AssemblyLine: public adevs::Network<int>
{
  public:
    AssemblyLine():
      adevs::Network<int>(),
      // Create the components
      press(1.0),drill(2.0){}

    void getComponents(adevs::Set<adevs::Atomic<int>*>& c)
    {
      c.insert(&press);
      c.insert(&drill);
    }
    void route(const int& value, adevs::Atomic<int>* model,
      adevs::Bag<adevs::Event<int> >& r)
    {
      adevs::Event<int> x;
~~~
```