```
class A {
    int result = 42;
    int f(int x) {
        if (x < 1)
            result = x;
        return result;
    }
    public static void main(String[] args) {
        A o = new B();
        int x = 2;
        int y = o.f(x);
    }
}
class B extends A{
    int f(int x) {
        if (x < 2)
            result = x;
            return result;
    }
}
class C extends A {
    int f(int x) {
        if (x < 3)
            result = x;
            return result;
    }
}
```

![](bbox=[0.278, 0.497, 0.722, 0.509])

basic terms essentially become implications on the object's runtime type. For the example program in Figure 5.6, the path condition between x and y on line 11 would be

> $PC(x,y) \equiv (o : A \Rightarrow PC_A(x,y)) \wedge (o : B \Rightarrow PC_B(x,y)) \wedge (o : C \Rightarrow PC_C(x,y)) (**)

In general, for a dynamically dispatched call y = o.f(x), the JLS [GSJB05] induces the following fundamental condition:

> $PC_t(x,y) = \bigvee_{i=1}^n (\gamma_i \Rightarrow PC_{\gamma_i,t}(x,y))$ (5.13)

An alternative formulation of this condition is:

> $PC_t(x,y) = \bigvee_{i=1}^n (|gamma_i \wedge PC_{\gamma_i,t}(x,y))$ (5.14)

**Theorem 5.1.** $O \neq$ null.

> $igwedge_{i=1}^n (\gamma_i \Rightarrow PC_{\gamma_i,t}(x,y)) \equiv \bigvee_{i=1}^n (\gamma_i \wedge PC_{\gamma_i,t}(x,y))$

^3 [HKS06] used 'instanceof' in the example, which might be misleading due to Java's instanceof operator. The formulae in this work present the exact semantics.