```
out << p.blue:
    return out;
}
/*...........................................*/
```

```
istream& operator>>(istream& in, Pixel& p)
{
    in >> p.red >> p.green >> p.blue;
    p.validate();
    return in;
}
/*...........................................*/
```

```
Pixel::Pixel()
{
    //Black
    red=green=blue=0;
    return;
}
/*...........................................*/
```

```
Pixel::Pixel(unsigned int value)
{
    //Gray scale
    red=green=blue=value;
    validate();
    return;
}
/*...........................................*/
```

```
Pixel::Pixel(unsigned int r,unsigned int g,unsigned int b)
{
    //Full color range
    red=r;
    green=g;
    blue=b;
    validate();
    return;
}
/*...........................................*/
```

```
bool Pixel::overflow() const
{
    return(overflowFlag&CHECK;
}
/*...........................................*/
```

```
void Pixel::reset()
{
    if(red > MAXVAL) red = MAXVAL;
    if(green > MAXVAL) green = MAXVAL;
    if(blue > MAXVAL) blue = MAXVAL;
    overflowFlag = 0;
}
```