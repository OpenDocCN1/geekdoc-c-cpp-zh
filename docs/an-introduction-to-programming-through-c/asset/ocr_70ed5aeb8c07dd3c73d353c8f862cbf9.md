```
cout << "Give the next number: ";
    cin >> num;
    maximum = max(maximum,num);
}
cout << "Maximum is: " << maximum << endl;
}
```

This program does not behave identically to the program sketched earlier, i.e. obtained by initializing maximum to - numeric_limits<float>::max(). The exercises ask you to say when the programs might differ, and which one you prefer under what circumstances.

# 3.4.2 Combining sequence generation and accumulation

Often we need to combine the sequence generation and accumulation idioms.

Suppose we want to compute n factorial, written as n!, which is just short hand for the product n × (n − 1) × (n − 2) × ⋯ × 2 × 1. How can we do this?

The key point to note is that we merely need to take the product of the sequence of numbers 1, 2, …, n−1, n, and this is a sequence that we can generate. But if we can generate a sequence, then we can easily take its product, i.e. accumulate it using the multiplication operator.

```
main_program{
    int n, fac=1, i=1;
    cin >> n;

    repeat(n){
        fac = fac * i;      // sequence accumulation
        i = i + 1;          // sequence generation
    }
    cout << fac << endl;
}
```

In the above program, if you ignore the statement fac = fac * i;, then we merely have our sequence generation program, with the sequence 1 to n being generated in the values taken by the variable i. However, the value generated in each iteration is being multiplied into the variable fac which was initialized to 1. Hence in the end the variable fac contains the product of the numbers from 1 to n, i.e. n! as we wanted. Note that the program also works for n=0, since 0! is defined to be 1.

The idioms of accumulation and sequence generation are very useful, and very, very commonly used. They are used so commonly that they will become second nature soon. We see a more involved example in Chapter 4.

# 3.5 Some operators inspired by the idioms

Because sequence generation and accumulation occur commonly in code, C++ includes operators that can be used to express these idioms more succinctly.