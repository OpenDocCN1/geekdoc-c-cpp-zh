class. But we also want the wheels to turn; this is accomplished by rotating them. Clearly, if the car moves forward by an amount dx, then the wheels must rotate by dx/r radians, where r is the radius of the wheels. But why does the rotate function called with an extra argument false? And why is the function repaint called? We explain these next.

# 24.3.4 Frames

Another detail of simplecpp graphics which we have withheld from you is that all the configuration change commands, i.e. forward, move, rotate and so on have an additional argument repaintP which takes the default value true. If repaintP is true, then the canvas is repainted as discussed in Section 24.2 after every configuration change. If repaintP is false, then the repainting is not done, only the configuration change is recorded.

This feature is useful especially when invoking a configuration change command on subobjects comprising a composite object. We do not want repainting to happen after a move of each subobject. It is inefficient and also causes visually annoying. Rather we want repainting to happen once, after the configuration change is recorded for all subobjects. This is what the code above accomplishes: no repainting happens after the Composite::forward as the two w...->rotate operations. Repainting is done only at the end unless it is disabled by the caller to Car::forward.

# 24.3.5 Main program

Finally, here is a main program that might use the above definitions.

```
int main(){
    initCanvas("Car",0,0,800,800);

    Car c(300,300,COLOR("blue"));
    Car d(300,600,COLOR("red"));
    d.scale(0.5);
    getClick();

    for(int i=0; i<100; i++){
        c.forward(3.0,false);
        d.forward(1.5,false);
        repaint();
    }
    getClick();
}
```

The main program creates two cars, one blue and another red. The red car is then scaled to half its size. This causes all the components of the car to shrink – this is handled automatically by the code in the Composite class.

Finally, we move the cars forward. When you execute this, the car wheels should appear to roll on the ground. Further, the wheels of the smaller car should appear to have twice as many rotations per unit time because the smaller wheel has half the radius but is travelling the same distance as the larger wheel.