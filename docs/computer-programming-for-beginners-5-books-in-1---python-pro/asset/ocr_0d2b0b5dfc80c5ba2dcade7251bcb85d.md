```
protected int height;
}

// PaintCost for the Base class
public interface PaintCost {
    int calculateCost(int area);
}
// The derived class
class Board : Object, PaintCost {
    public int calculateArea() {
        return (width * height);
    }
    public int calculateCost(int area) {
        return area * 120;
    }
}
class InheritanceTester {
    static void Main(string[] args) {
        Board B = new Board();
        int area;
        B.setWidth(5);
        B.setHeight(7);
        area = B.calculateArea();
        // Show the area of the object
        Console.WriteLine("The area of the object is: {0}",
            B.calculateArea());
        Console.WriteLine("The total printing cost is: ${0}",
            B.calculateCost(area));
        Console.ReadKey();
    }
}
```

The code gives the following output: