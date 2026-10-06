# Bioinformatics challenges at the interface of biology and computer science

bubble rising to the top of a volume of water – hence the name, bubble sort. A naive formulation of the bubble sort algorithm is described in pseudocode in Figure 6.7 – we recommend that you scrutinise its details, as it forms the basis of subsequent discussions.

We have a basis for introducing few more efficient algorithms. First, although the idea of swapping two numbers is obviously a simple one, the reality is that it's impossible for a computer to atomically transpose two memory values. The computer must copy the value from the first item elsewhere, before overwriting it with the second value, then finally overwriting the second item with the temporarily stored value. Triangular rotation of values is always required in such cases: even if our preferred programming language provides a swap(a,b) function, it will still be performing the three-step process under the hood, taking longer and using more memory than we might expect. Understanding what lies beneath a language's abstractions can mean the difference between an algorithm completing in the blink of an eye, and taking longer than our concentration span.

Second, although it not be obvious at first, roughly half the total number of comparisons (line 11 in Figure 6.7) will always return false. After the first pass, the final item is necessarily the largest value in the list; therefore, on the next pass the last two values are guaranteed to be in the correct order; there's no need to check them. In each subsequent pass, values are bubbled into their correct order, increasing the number of comparisons, which wastes processor time and slows the algorithm's execution.

More subtly, bubble sort exhibits stable sorting, thus that values are considered equal remain in relative order to each other once the list has been processed. If a different algorithm had been chosen that didn't exhibit stable sorting, difficulties in the program in which it was used might arise from these unexpected side-effects.

Finally, one interesting feature of any algorithm is its progression changes depending on the nature of its input. If the input to our bubble sort were already in true order, we could observe that there were no swaps during the first pass and simply stop the execution, the rest of the passes having become superfluous. Conversely, if the input were in reverse order to begin with, this algorithm would pathologically perform

```
1 function swap(integer a, integer b):
2   let t=a
3   a=b
4   b=t
5 end function
6
7 function sort(list 1)
8   let n=length(1)
9   repeat n-1 times:
10    for each element in [0, n-2] as i:
11      if L[i] > L[i+1]:
12        swap(L[i], L[i+1])
13      end if
14    end for
15  repeat
16 end function
```

# Figure 6.7

Pseudocode for a naive formulation of the bubble sort algorithm. Following the programming convention, zero-based indices are used to show the items in the list: L[0] would be the first item of the list, and L[n-1] the last item in a list of length n.