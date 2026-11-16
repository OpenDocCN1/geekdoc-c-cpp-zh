```
int calculate_base_area();
};
int base_area::calculate_base_area()
{
    return length*breadth;
}
```

```
class side_area:public base_area
{
    public:
    int calculate_side_area();
};
```

```
int side_area::calculate_side_area()
{
    return length*height;
}
```

```
int main()
{
    class side_area s1;
    cout<<""Volume of cuboid is: "<"<s1.volume(2,3,4)<<endl;
    cout<<""Base area of cuboid is: "<"<s1.calculate_base_area()<<endl;
    cout<<""Area of side wall of cuboid is: "<"<s1.calculate_side_area());
}
```

Output
Volume of cuboid is: 24
Base area of cuboid is: 6
Area of side wall of cuboid is: 8