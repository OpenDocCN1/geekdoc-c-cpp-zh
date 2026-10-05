You will find the &z sequence twice in the example. I would like to point out that it has different meanings depending on the context. &z in push_back(&z) means “address of z,” but in the for(Number &z :...) loop, it reads as “z is of type reference to Number.” Another interesting point is the following:

```
Number two{2};
primes.push_back(&two); // the 2 is needed
```

Because allNumbers initially contains only numbers starting from 3, you don't have an object in allNumbers for the first prime number—whose address you can store in primes. But you don't need with pointers. You can take the addresses of objects that are located anywhere in memory. The Number two{2}; variable is an object with an address that immediately goes into primes.

You see that when storing addresses, you are by no means limited to obtaining your raw pointers from just one source. You just need to make sure that all sources exist as long as the stored numbers.

So what should you absolutely avoid doing? primes returning as a result, like in Listing_20.9. There, the source objects with allNumbers were destroyed upon leaving the function. The pointers you stored in primes for return primes; are no longer valid outside the function. Dereferencing them is then prohibited and best leads to a program crash.

```
vector<Number*> primePointers(unsigned long upTo) { // Vector of * is suspicious
```