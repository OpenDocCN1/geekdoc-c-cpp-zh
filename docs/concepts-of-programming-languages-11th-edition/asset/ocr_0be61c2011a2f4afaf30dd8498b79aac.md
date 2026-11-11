Note that `>>` is the prompt of the interactive Ruby interpreter and `=>` is used to indicate the return value of the expression. The Ruby `puts` statement displays its parameter. In this example, the `times` method is sent to the object `4`, with the block sent along as a parameter. The `times` method calls the block four times, producing the four lines of output. The destination object, `4`, is the return value from `times`.

The most common Ruby iterator is `each`, which is often used to go through arrays and apply a block to each element.⁵ For this purpose, it is convenient to allow blocks to have parameters, which, if present, appear at the beginning of the block, delimited by vertical bars (`|`). The following example, which uses a block parameter, illustrates the use of `each`:

```
>> list = [2, 4, 6, 8]
=> [2, 4, 6, 8]
>> list.each {|value| puts value}
2
4
6
8
=> [2, 4, 6, 8]
```

In this example, the block is called for each element of the array to which the `each` method is sent. The block produces the output, which is a list of the array's elements. The return value of `each` is the array to which it is sent.

Instead of a counting loop, Ruby has the `upto` method. For example, we could have the following:

```
1.upto(5) {|x| print x, " "}
```

This produces the following output:

```
1 2 3 4 5
```

Syntax that resembles a **for** loop in other languages could also be used, as in the following:

```
for x in 1..5
  print x, " "
end
```

Ruby actually has no **for** statement—constructs like the above are converted by Ruby into `upto` method calls.

⁵ This is similar to the `map` functions discussed in Chapter 15.