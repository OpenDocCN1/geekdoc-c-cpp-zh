```
    // ...\n}\n);\n\ntemplate<typename T1, typename T2>\npair<T1,T2> make_pair(T1 x, T2 y)\n{\n\t\treturn {x,y};\n}
```

We copied the complete definition of pair and its useful helper function make_pair() from the standard.

Note that when you iterate over a map, the elements will come in the order defined by the key. For example, if we iterated over the fruits in the example, we would get

(Apple,7) (Grape,2345) (Kiwi,100) (Orange,99) (Plum,8) (Quince,0)

The order in which we inserted those fruits doesn’t matter.

The insert() operation has an odd return value, which we most often ignore in simple programs. It is a pair of an iterator to the (key,value) element and a bool which is true if the (key,value) pair was inserted by this call of insert(). If the key was already in the map, the insertion fails and the bool is false.

Note that you can define the meaning of the order used by a map by supplying a third argument (Cmp in the map declaration). For example:

```
map<string, double, No_case> m;
```

No_case defines case-insensitive compare; see §21.8. By default the order is defined by less<Key>, meaning “less than.”

# 21.6.3 Another map example

To better appreciate the utility of map, let’s return to the Dow Jones example from §21.5.3. The code there was correct if and only if all weights appear in the same position in their vector as their corresponding name. That’s implicit and could easily be the source of an obscure bug. There are many ways of attacking that problem, but one attractive one is to keep each weight together with its company’s ticker symbol, e.g., (“AA”,2.4808). A “ticker symbol” is an abbreviation of a company name used where a terse representation is needed. Similarly we can keep the company’s ticker symbol together with its share price, e.g., (“AA”,34.69). Finally,