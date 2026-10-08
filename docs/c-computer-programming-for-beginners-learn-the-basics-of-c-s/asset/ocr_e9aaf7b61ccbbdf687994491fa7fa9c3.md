```
double volume;

// Declare Box2 of type Box
// box 1 specification
Box1.setLength(6.0);
Box1.setBreadth(7.0);
Box1.setHeight(5.0);
// box 2 specification
Box2.setLength(12.0);
Box2.setBreadth(13.0);
Box2.setHeight(10.0);
// volume of box 1
volume = Box1.getVolume();
Console.WriteLine("Volume of Box1 : {0}",volume);
// volume of box 2
volume = Box2.getVolume();
Console.WriteLine("Volume of Box2 : {0}", volume);
Console.ReadKey();

}
}
```

On executing the code given above, the following result will be produced.

Volume of Box1 : 210