This is why it is stored here in a local variable named "X3J" that is initialized with a trivial zero value and is then given a more meaningful value in the second loop on 'i' = 0,1,2,3 in Section A.32. More precisely, "X3J" stores the three-dimensional vector ∫∫∫_T vψ_i at the end of Section 31.4:

```
for(int i=0; i<4; i++){
    int I = (*runner)()[i].getIndex();
    point3 X3J(0.,0.,0.);
    for(int j=0; j<4; j++){
        int J = (*runner)()[j].getIndex();
        double integralPij =
            i == j ?
            1/60.
            :
            1/120.;
        for(int jblock=0;jblock<3;jblock++)
            X3J(jblock) += integralPij *
                x[J+jblock*nodes][0];
    }
}
```

Note that, in the above right-hand side, 'x' is the "dynamicVector<point>" argument that is passed by reference to the present constructor in Section A.32. This is why the first call to "operator[]" (defined in Section 3.3) returns its "point" component that corresponds to block "jblock" and to node 'j' in the current tetrahedron (or node 'J' in the list of nodes in the entire mesh). The second call to "operator[]", on the other hand, is defined in Section 2.18, and thus returns the real part of the complex number represented by this "point" object. (Although the Navier–Stokes system is real, so 'x' could actually be of type "dynamicVector<double>" rather than "dynamicVector<point>", we prefer to stick to the original code in Section A.32 in which the elements in the stiffness matrix are 2 × 2 block matrices rather than scalars.)

We are now ready to assemble the last term at the end of Section 31.4:

```
for(int j=0; j<4; j++){
    int J = (*runner)()[j].getIndex();
    double integralPij =
        i == j ?
        1/60.
        :
        1/120.;
    T addIJ = X3J *
        (SinverseTdetS * gradient[j]);
    if(this->item[I+iblock*nodes]){
        row<T> r(addIJ,J+iblock*nodes);
        *this->item[I+iblock*nodes] += r;
    }
    else
        this->item[I+iblock*nodes] =
            new row<T>(addIJ,J+iblock*nodes);
}
```