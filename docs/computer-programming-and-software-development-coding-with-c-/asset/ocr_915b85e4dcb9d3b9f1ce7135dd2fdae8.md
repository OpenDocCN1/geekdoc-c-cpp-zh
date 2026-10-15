```
using System;

namespace Polygons.Library
{
    public class Triangle : AbstractRegularPolygon
    {
        public Triang
            base(3, l
        { }

        //public over
        //{
        //    return SideLength * SideLength * Math.Sqrt(3) / 4;
        //}
    }
}
```

Let's take a look at an interface. And for that, we'll look at the IRegularPolygon interface. One thing to notice is that the name of our interface starts with a capital letter I. This is done by convention. There's nothing that forces you to do this, but all of the interfaces in the .NET library start with a capital letter I, so I follow that same convention. Our interface is interesting because in this case, it contains declarations only. It does not contain implementation code, and this is where things get a little confusing. Remember how I kept mentioning automatic properties. Well, if we look at the code we have here for a NumberOfSides and SideLength, it certainly looks like an automatic property, but it is not. This is a declaration that whoever implements this interface must provide these two properties. Typically, interfaces do not contain implementation, code. It is up to the implementing classes to provide that. Interfaces can provide a default implementation that will be used if the class does not provide one; however, this feature has some additional concerns. We will explore this in the last chapter of the book. Until then, the interfaces in our examples will not have any implementation, and specifically, with regard to properties, there's no way to put an