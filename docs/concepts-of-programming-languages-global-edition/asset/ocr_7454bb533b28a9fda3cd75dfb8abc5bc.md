```
public class A {
	public int a, b;
	public void draw() { . . . }
	public int area() { . . . }
}

public class B extends A {
	public int c, d;
	public void draw() { . . . }
	public void sift() { . . . }
}
```

The CIRs for the A and B classes, along with their vtables, are shown in Figure 12.7. Notice that the method pointer for the area method in B's vtable points to the code for A's area method. The reason is that B does not override A's area method, so if a client of B calls area, it is the area method inherited from A. On the other hand, the pointers for draw and sift in B's vtable point to B's draw and sift. The draw method is overridden in B and sift is defined as an addition in B. Multiple inheritance complicates the implementation of dynamic binding. Consider the following three C++ class definitions:

```
class A {
	public:
	int a;
	virtual void fun() { . . . }
	virtual void init() { . . . }
};
```

![](bbox=[0.52, 0.26, 0.95, 0.78])

> An example of the CIRs with single inheritance