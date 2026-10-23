```
Vector b2(J-1, -2.0);
Vector c2(J-1, 1.0);
Vector r2(J-1, -2.0*h*h);      // Right-hand side

// Take the boundary conditions into consideration
r2[0] -= BCL;
r2[r2.size()-1] -= BCR;

LUTridiagonalSolver<double> mySolver2(a2, b2, c2, r2);
std::cout << "Matrix has a solution? "
<< mySolver2.diagonallyDominant() << '\n';
DoubleSweep<value_type> mySolver(a, b, c, r, BCL, BCR);

StopWatch<> sw;
sw.Start();
Vector result = std::move(mySolver());
Vector result2 = std::move(mySolver2());
sw.Stop();
std::cout << "Elapsed time: " << sw.GetTime() << '\n';

auto exact = [](double x) { return x*(1.0 - x); };
double val = h;            // Double Sweep

// Compare output from Double Sweep and Thomas with each other
for (std::size_t j = 1; j < result.size()-1; ++j)
{ // The values should be zero

    std::cout<< j << ", " << result[j]-result2[j-1] <<",
"<< exact(val)<< '\n';
    val += h;
}
return 0;
}
```

We note the difference in how the two algorithms handle the boundary values. This is worth stressing as we need to be clear on how to incorporate the Dirichlet boundary conditions into the algorithms. This is an important skill as you will need to be able to perform the same trick for more complicated problems in later chapters.

# 13.2.4 Performance Issues

We might consider improving the run-time performance of the algorithms in Sections 13.2.1 and 13.2.2. In their current form we have seen that the Double Sweep algorithm is approximately 20% more efficient than the Thomas algorithm (this might be due to the fact that the latter uses three work arrays while the former has been programmed using two work arrays). We also carried out some tests using the Boost Pool library (for fast memory allocation) which improves run-time efficiency even more. We have stress tested these solvers when applied to the diffusion equation (which we shall discuss in Section 13.3) using mesh sizes of 100,000 in both space and time. Both methods give accurate results. The processing times on a normal laptop in seconds were in the ranges [490, 588] for Double Sweep and [730, 780] for the Thomas algorithm.