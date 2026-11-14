```
//File: convolve.c
//Function: conv2d
...
10. /* Convolve the input image with the kernel. */
11. for(int r = 0; r<kN-1; ++) {
12. for(int c = 0; c<kN-1; ++) {
13. sum = 0;
14. for(int i = 0; i<k; i++) {
15. for(int j = 0; j<k; j++) {
16. sum += input_image[r+i][c+j] * kernel[i][j];
17. }
18. }
19. output_image[r-dead_rows][c+dead_cols] = (sum / normal_factor);
20. }
21. }
--
```

Fig. 3.27 C code section for the MATLAB code for a 2D convolution of an input image with a kernel.

```
select loop end
apply
    printfn("Found loop of type: " + $loop.type);
end
```

Fig. 3.28 Querying loops and reporting their type (i.e., for, while, do while).

code mixed with specific LARA constructs. Fig. 3.28 shows an example where for each loop in the code the weaver prints to the console the type of each loop found. To access information about the program element, the join point can be used in the apply section by prefixing its name with $ (Sloop in the example shown). In order to access an attribute of a specific join point, the name of the attribute prefixed by "$" must be followed by "." and by the name of the attribute (e.g., Sloop.type). When the aspect is applied to the code in Fig. 3.27, the output is as follows:

Found loop of type: for
Found loop of type: for
Found loop of type: for
Found loop of type: for

If the printfn statement is replaced by printfn("Is innermost? " + $loop.is_innermost); the result is as follows:

Is innermost? false
Is innermost? false
Is innermost? false
Is innermost? true

The semantics of a select-apply section resembles that of a query language. For each program element found by the select statement, the corresponding code of the apply section is executed. In the example shown in Fig. 3.28, the code does not