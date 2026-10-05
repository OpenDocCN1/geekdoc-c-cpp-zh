# Classes and Objects 41

After

```
int getFeet(Distance * const);
```

Before

```
void setInches(float);
```

After

```
void setInches(Distance * const, float);
```

Before

```
float getInches();
```

After

```
float getInches(Distance * const);
```

+   3. It puts the definition of this pointer as a leading formal argument in the definitions of all member functions as follows. It also modifies all the statements to access objects by accessing them through this pointer using pointer-to-member access operator (->).

Before

```
void Distance::setFeet(int x)
{
  iFeet=x;
}
```

After

```
void setFeet(Distance * const this, int x)
{
  this->iFeet=x;
}
```

Before

```
int Distance::getFeet()
{
  return iFeet;
}
```

After

```
int getFeet(Distance * const this)
{
  return this->iFeet;
}
```

Before

```
void Distance::setInches(float y)
{
  fInches=y;
}
```

After

```
void setInches(Distance * const this, float y)
```