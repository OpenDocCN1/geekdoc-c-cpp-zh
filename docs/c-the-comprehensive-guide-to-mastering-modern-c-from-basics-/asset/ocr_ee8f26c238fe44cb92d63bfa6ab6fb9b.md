In if(factor*factor > n) and if(n%factor==0), you see it without braces. The same applies to for.

```
for(int prime : primes)    // for followed by a single statement
std::cout << prime << " ";
std::cout << " "; // not part of anymore
```

# **Listing 8.2** This "for" refers to only one statement.

The for is only coupled with the first of the two outputs. The second line is output only once. If you wanted to do more things within the loop, then use {...}. This way, you get a statement block that counts as a single statement for the for.

```
for(int prime : primes){ // Beginning of the block
std::cout << prime;
std::cout << " "; // End of the block
}
std::
```

# **Listing 8.3** A statement block is enclosed in ( and ).

Now the separated cout outputs are both executed within the loop.

# Howe 8.1.1 Standalone Blocks and Variable Scope

don't have to bind blocks to a for or similar; you can introduce them anywhere it makes sense to you instead of a single statement. The following listing is an example of this.