```
case Pathliterator.SEG_MOVETO:
    System.out.println( "SEG_MOVETO: " + point );
    break;
case Pathliterator.SEG_LINETO:
    System.out.println( "SEG_LINETO: " + point );
    break;
case Pathliterator.SEG_QUADTO:
    System.out.println( "SEG_QUADTO: " + point );
    break;
case Pathliterator.SEG_CUBICTO:
    System.out.println( "SEG_CUBICTO: " + point );
    break;
case Pathliterator.SEG_CLOSE:
    System.out.println( "SEG_CLOSE: " + point );
    break;
}
pit.next();
}
```

# RESOURCES AND FURTHER READING

Akenine-Moller, Tomas and Eric Haines, Real-Time Rendering. 2nd Edition, A K Peters, 2002.

Ericson, Christer, Real-Time Collision Detection, Focal Press, 2004.