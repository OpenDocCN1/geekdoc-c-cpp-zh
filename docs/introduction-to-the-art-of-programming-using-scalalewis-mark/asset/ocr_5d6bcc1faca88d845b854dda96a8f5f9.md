|  | data.length*2 |  | data.length+10 |  |
|---|---|---|---|---|
| Resize Event | Size | Total Work | Size | Total Work |
| 1 | 10 | 10 | 10 | 10 |
| 2 | 20 | 30 | 20 | 30 |
| 3 | 40 | 70 | 30 | 60 |
| 4 | 80 | 150 | 40 | 100 |
| 5 | 160 | 310 | 50 | 150 |
| 6 | 320 | 630 | 60 | 210 |
| ... | ... | ... | ... | ... |
| m | 10 × 2^m | 10 × (2^{m+1} − 1) | 10m | 5m(m + 1) |

To get the amortized cost, we divide the total work by the size because we had to call push that number of times to get the stack to that size. For the first approach we get

```
\frac{10 \times (2^{m+1} - 1)}{10 \times 2^{m}} = \frac{2^{m+1} - 1}{2^{m}} = 2 - \frac{1}{2^{m}} \approx 2 \in O(1).
```

For the second approach we get

```
\frac{5m(m + 1)}{10m} = \frac{m + 1}{2} \in O(m).
```

Neither the multiple of 2, nor the addition of 10 is in any way magical. Growing the array by a fixed multiple greater than one will lead to amortized constant cost. Growing the array by any fixed value will lead to an amortized linear cost. The advantage of the fixed multiple is that while the copy events gets exponentially larger, they happen inversely exponentially often.

# Manifests (Advanced)

To understand Manifests, it helps to have some understanding of the history of Java as the nature of the Java Virtual Machine (JVM) plays a role in their existence. The parallel to Scala type parameters in Java is generics. Generics did not exist in the original Java language. In fact, they were not added until Java 5. At that point, there were a huge number of JVMs installed around the globe and it was deemed infeasible to make changes that would invalidate all of them. For that reason, as well as a motivation to keep the virtual machine fairly simple, generics were implemented using erasure. What this means is that the information for generics was used at compile time, but was erased in the compiled version so that at runtime it was impossible to tell what the generic type had been. In this way, the code that was produced looked like what would have been produced before generics were introduced.

This has quite a few effects on how Java programs are written. It comes through in Scala as a requirement for having a manifest on certain type parameters. The manifest basically holds some of the type information so that it is available at runtime. To understand why we need this, we should go back to the expression that was responsible for us needing a manifest: new Array[A](10). This makes a new Array[A] with 10 elements in it and sets the 10 elements to appropriate default values. It is the last part that leads to the requirement of having a manifest. For any type that is a subtype of AnyRef, the default value is null. For the subtypes of AnyVal, the default varies. For Int, it is 0. For Double it is 0.0. For Boolean it is false. In order to execute that expression, you have to know enough at least enough about the type to put in