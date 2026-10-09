# ### 18.1 typedef

We have already seen that the names of types in C++ can become very long. For example, we have already had to work with the following member variable of the Portfoliolmpl class.

```
vector< shared_ptr<Priceable> > securities;
```

C++ contains a number of features that help with dealing with long type names. One is typedef, which we shall discuss now, a second is auto, which we shall discuss in the next section.

typedef allows you to define an abbreviation for a complex type. For example, we can define an abbreviation for a shared pointer to a Priceable as follows.

```
typedef std::shared_ptr<Priceable> SPPriceable;
```

The syntax looks as though we are declaring a variable called SPPriceable of type shared_ptr<Priceable> except for the keyword typedef in front. In other words, the syntax is:

```
typedef <<Complex Type>> <<Abbreviation>>;
```

Having defined this abbreviation, we can now rewrite the declaration of the member variable securities as:

```
vector<SPPriceable> securities;
```

The advantage of typedef in terms of reducing the amount of typing is clear. By making the code shorter, it also makes it more readable. However, excessive use of typedef will make your code harder to understand and debug. Each use of typedef introduces something extra for the reader of your code to remember.

Personally I find that the convention of having type names beginning SP to abbreviate shared_ptr is both convenient and easy to remember. I also use a prefix of SPC to mean a const pointer such as:

```
typedef std::shared_ptr<const Priceable> SPPriceable;
```

We will use these conventions without comment from now on, although they are by no means a standard convention in C++.

Unless you have such clear conventions, it is best to avoid putting typedef declarations at the top level in a header file. This is because it is often more confusing than helpful. Within a cpp file you can allow yourself more freedom because you only need to remember the abbreviation you are using within the file.