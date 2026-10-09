```
IPerimeter.Size().</summary>
float IPerimeter.Size() => 230.0f;
}
/// <summary>
/// ShapeD illustrates multiple interface inheritance.
/// It includes explicit implementations of IArea.Size() and
IPerimeter.Size().
/// It also includes a method Size() with the same name and signature.
//</summary>
public class ShapeD : IArea, IPerimeter {
/// <summary>It has nothing to do with IArea.Size() or
IPerimeter.Size().</summary>
public float Size() => 240.0f;
/// <summary>An explicit implementation of IArea.Size().</summary>
float IArea.Size() => 250.0f;
/// <summary>An explicit implementation of
IPerimeter.Size().</summary>
float IPerimeter.Size() => 260.0f;
}
/// <summary>
/// ShapeE illustrates multiple interface inheritance.
/// It includes an explicit implementation for IArea.Size().
//</summary>
public class ShapeE : IArea, IPerimeter {
/// <summary>An explicit implementation of IArea.Size().</summary>
float IArea.Size() => 270.0f;
}
/// <summary>
/// ShapeF illustrates multiple interface inheritance.
/// It includes an explicit implementation for IPerimeter.Size().
//</summary>
public class ShapeF : IArea, IPerimeter {
/// <summary>An explicit implementation of
IPerimeter.Size().</summary>
```