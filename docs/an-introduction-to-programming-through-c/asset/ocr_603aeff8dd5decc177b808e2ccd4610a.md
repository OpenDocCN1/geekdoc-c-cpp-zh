composite object, and hence must be owned by the composite object. Thus an important step in defining a composite object is to declare it to be the owner of the contained objects.

To do this, the constructor of every graphical object is provided with an optional argument named owner. This argument takes value NULL by default which simplecpp interprets to mean the canvas. Thus so far we did not tell you about this argument, and you didnt not specify the value, and hence simplecpp made the canvas the owner of all the objects you created. If you want to indicate a different owner, you instead pass a pointer to that owner. Since we create contained objects in the body of the composite, we must pass a pointer to the composite object itself. As you know, inside the definition of an object, the keyword this denotes a pointer to the object. So the extra argument must have this as its value.

# 24.3.2 The Composite class constructor

The Composite class constructor has the following signature.

```
Composite(double x, double y, Composite* owner=NULL)
```

Here the last argument owner gives the owner of the composite object being defined, and x,y give the coordinates of the composite object in the frame of its owner. As mentioned earlier, if you do not specify this argument, it is taken as NULL, indicating that the canvas is the owner. The owner argument must be specified if this composite object is itself a part of another composite object. This kind of containment is allowed and we will see an example shortly.

# 24.3.3 A Car class

We now construct a Car class. Our car will consist of a polygonal body, and two wheels. We will give the wheels some personality by adding in spokes. So we will model a car as a composite object, consisting of the body and the wheels. But note that a wheel itself contains a circle representing the rim, and lines representing the spokes. So the wheel will itself have to be represented as a composite object. Note that we allow one composite object (e.g. a car) to contain other ordinary objects (e.g. body) or other composite objects (e.g. wheels).

We begin by defining a class for wheels.

```
class Wheel : public Composite{
    Circle *rim;
    Line *spoke[10];
public:
    Wheel(double x, double y, Composite* owner=NULL) : Composite(x,y,owner) {
        rim = new Circle(0,0,50,this);
        for(int i=0; i<10; i++){
            spoke[i] = new Line(0, 0, 50*cos(i*PI/5), 50*sin(i*PI/5), this);
        }
    }
};
```