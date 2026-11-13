```
case 3:
    prefixtoinfix();
    break;
case 4:
    prefixtopostfix();
    break;
default:
    cout << "\n\nSorry, wrong choice";
}
while(choice < 5);
getch();
}
```

# 3.9 PROCESSING OF FUNCTION CALLS

One natural application of stacks, which arises in computer programming, is the processing of function calls and their terminations. The program must remember the place where the call was made so that it can return there after the function is complete. Suppose we have three functions, say, A, B, and C, and one main program. Let the main invoke A, A invoke B, and B in turn invoke C. Then, B will not have finished its work until C has finished and returned. Similarly, main is the first to start work, but it is the last to be finished, not until sometime after A has finished and returned. Thus, the sequence by which a function actively proceeds is summed up as the LIFO or FILO property, as shown in Fig. 3.14. The output is shown in Fig. 3.15.

From the output in Fig. 3.15, it can be observed that the main program is invoked first but finished last, whereas the function C is invoked last but finished first. Hence, to keep track of the return addresses ra, rb, and rc the only data structure required here is the stack.

![](bbox=[0.245, 0.705, 0.885, 0.905])

Fig. 3.14 Processing of function calls