# Adding Two Distance Objects

Now, let's add a new member function:

```
AddDist()
```

that adds two Distance objects together.

```
// dist2.h

#ifndef DIST2_H
#define DIST2_H

class Distance {
private:
    int feet;
    float inches;
public:
    void setDist(int ft, float in);
    void getDist();
    void showDist();
    void addDist(Distance d1, Distance d2);
};

#endif
```