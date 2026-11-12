```
}
else
{
    a[tid] += b[tid] * c[tid];
    }
}
}
```

Here we have set up a number of kernels, each of which exhibit different levels of divergence. The first is the optimal with no divergence. The second diverges based on half-warps. These half-warps should execute in parallel. We then further subdivide the first half-into two groups. These should execute in series. We then subdivide again the first group into a total of four serial execution paths. The results we see are as follows:

ID:0 GeForce GTX 470:Running 32768 blocks of 32 threads to calculate 1048576 elements
ID:0 GeForce GTX 470:All threads : 27.05 ms (100%)
ID:0 GeForce GTX 470:Half warps : 32.59 ms (121%)
ID:0 GeForce GTX 470:Quarter warps : 72.14 ms (267%)
ID:0 GeForce GTX 470:Eighth warps : 108.06 ms (400%)

ID:1 GeForce 9800 GT:Running 32768 blocks of 32 threads to calculate 1048576 elements
ID:1 GeForce 9800 GT:All threads : 240.67 ms (100%)
ID:1 GeForce 9800 GT:Half warps : 241.33 ms (100%)
ID:1 GeForce 9800 GT:Quarter warps : 252.77 ms (105%)
ID:1 GeForce 9800 GT:Eighth warps : 285.49 ms (119%)

ID:2 GeForce GTX 260:Running 32768 blocks of 32 threads to calculate 1048576 elements
ID:2 GeForce GTX 260:All threads : 120.36 ms (100%)
ID:2 GeForce GTX 260:Half warps : 122.44 ms (102%)
ID:2 GeForce GTX 260:Quarter warps : 149.60 ms (124%)
ID:2 GeForce GTX 260:Eighth warps : 174.50 ms (145%)

ID:3 GeForce GTX 460:Running 32768 blocks of 32 threads to calculate 1048576 elements
ID:3 GeForce GTX 460:All threads : 43.16 ms (100%)
ID:3 GeForce GTX 460:Half warps : 57.49 ms (133%)
ID:3 GeForce GTX 460:Quarter warps : 127.68 ms (296%)
ID:3 GeForce GTX 460:Eighth warps : 190.85 ms (442%)

We can see this somewhat better in a graphical format in Figure 9.32.

Notice how the thread divergence is not such a significant problem on the compute 1.x devices (the 9800 GT and GTX260). It has an effect, but takes the maximum time to just 145% of the optimal time. By comparison, the Fermi compute 2.x cards (GTX460, GTX470) suffer over a 4× slowdown when diverging significantly within a warp. The GTX460 seems especially sensitive to warp divergence. Notice the GTX470 is almost 10× faster in absolute terms than the 9800 GT when there is no divergence, which is a massive improvement for just two generations of cards.

If you are curious to know how much a 32-way divergence costs, it leads to a 27× slowdown on the compute 1.x cards and a massive 125× to 134× slowdown on the compute 2.x cards. Note that the