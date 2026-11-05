```
namespace Acme
{
    class Widget: IProcess
    {
        public static explicit operator int(Widget x) {...}
        public static implicit operator long(Widget x) {...}
    }
}
```

"M:Acme.Widget.op_Explicit(Acme.Widget)~System.Int32"
"M:Acme.Widget.op_Implicit(Acme.Widget)~System.Int64"

# A.4 An example

# A.4.1 C# source code

The following example shows the source code of a Point class:

```
namespace Graphics
{
    
    /// <summary>Class <c>Point</c> models a point in a two-dimensional plane.
    /// </summary>
    public class Point
    {
        /// <summary>Instance variable <c>x</c> represents the point's
        /// x-coordinate.</summary>
        private int x;
        /// <summary>Instance variable <c>y</c> represents the point's
        /// y-coordinate.</summary>
        private int y;
        
        /// <value>Property <c>X</c> represents the point's x-coordinate.</value>
        public int X
        {
            get { return x; }
            set { x = value; }
        }
        
        /// <value>Property <c>Y</c> represents the point's y-coordinate.</value>
        public int Y
        {
            get { return y; }
            set { y = value; }
        }
        
        /// <summary>This constructor initializes the new Point to
        /// (0,0).</summary>
        public Point() : this(0,0) {}
        
        /// <summary>This constructor initializes the new Point to
        /// <paramref name="xor"/><paramref name="yor"/></summary>
        /// <param><c>xor</c> is the new Point's x-coordinate.</param>
        /// <param><c>yor</c> is the new Point's y-coordinate.</param>
        public Point(int xor, int yor) {
            X = xor;
            Y = yor;
        }
    }
```