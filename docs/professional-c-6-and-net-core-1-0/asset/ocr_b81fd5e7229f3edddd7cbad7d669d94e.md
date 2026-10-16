# WhatsNewAttributes

Now for the code for the vector class. You are not making any major changes to this class; you only add a couple of LastModified attributes to mark the work that you have done on this class in this chapter:

```
```csharp
namespace VectorClass
{
	[LastModified("6 Jun 2015","updated for C# 6 and .NET Core")]
	[LastModified("14 Deb 2010","IEnumerable interface implemented:" + "Vector can be treated as a collection")]
	[LastModified("10 Feb 2010","IFormattable interface implemented" + "Vector accepts N and VE format specifiers")]
	public class Vector : IFormattable, IEnumerable<double>
	{
		public Vector(double x, double y, double z)
		{
			X = x;
			Y = y;
			Z = z;
		}
		public Vector(Vector vector)
			: this (vector.X, vector.Y, vector.Z)
		{
		}
		public double X { get; }
		public double Y { get; }
		public double Z { get; }
		public string ToString(string format, IFormatProvider formatProvider)
		{
			//...
		}
	}
}
```
```

You also mark the contained VectorEnumerator class as new:

```
```csharp
[LastModified("6 Jun 2015",
"Changed to implement the generic interface IEnumerator<T>")]
[LastModified("14 Feb 2010",
"Class created as part of collection support for Vector")]
private class VectorEnumerator : IEnumerator<double>
{
}
```
```

That’s as far as you can get with this example for now. You are unable to run anything yet because all you have are two libraries. After taking a look at reflection in the next section, you will develop the final part of the example, in which you look up and display these attributes.