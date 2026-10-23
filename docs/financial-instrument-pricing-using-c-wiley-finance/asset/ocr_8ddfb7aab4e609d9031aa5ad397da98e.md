```
{
    return int(c); // simple test
};

SendAndReceive(converter);        // Converter is a message buffer

long relation (long n)
{
    if (n < 2) return n;

    return relation(n - 1) + relation(n - 2);
}
```

We conclude this section by introducing the choice and join classes. Both options are concerned with the processing of a set of messages. In the first case the first function to finish is selected (select among competing tasks) while in the second case all functions are selected:

```
// Choice: select the first available messages from a set of sources
concurrency::overwrite_buffer<long> rel1;
concurrency::overwrite_buffer<long> rel2;
concurrency::single_assignment<long> rel3;

auto selectOne = concurrency::make_choice(&rel1, &rel2, &rel3);

concurrency::parallel_invoke(
    [&rel1] {concurrency::send(rel1, relation(22)); },
    [&rel2] {concurrency::send(rel2, relation(14)); },
    [&rel3] {concurrency::send(rel3, relation(13)); }
);

// See who responds first
switch (concurrency::receive(selectOne))
{
case 0:
    std::cout << "rel1 " << concurrency::receive(rel1) << '\n';
    break;
case 1:
    std::cout << "rel2 " << concurrency::receive(rel2) << '\n';
    break;
case 2:
    std::cout << "rel3 " << concurrency::receive(rel3) << '\n';
    break;
default:
    std::cout << "oops\n";
    break;
}
```

```
// Run multiple tasks
concurrency::single_assignment<long> relA;
concurrency::single_assignment<long> relB;
concurrency::single_assignment<long> relC;

auto joinAll = concurrency::make_join(&relA, &relB, &relC);
```