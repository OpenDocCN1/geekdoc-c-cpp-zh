```
}
console.log(remove(["a", "k", "c", "f", "e"], 2));
// → ["a", "k", "f", "e"]
```

# Strings and their properties

During the string value chapter, we discussed length and toUpperCase but if you want to add a new property, it does not stick.

```
let kim = "Kim";
kim.age = 88;
console.log(kim.age);
// → undefined
```

All strings value contains a few methods. Some are the slice and indexOf which have a similar appearance of array methods as well as the name.

```
console.log("coconuts".slice(4, 7));
// → nut
console.log("coconut".indexOf("u"));
// → 5
```

A string’s indexOf can look for a string holding more than one character, while the corresponding array method search for a single element.

```
console.log("one two three".indexOf("ee"));
// → 11
```

The trim method eradicates whitespace from the beginning to the end of a string.

```
console.log(" okay \n ".trim());
// → okay
```

The zeroPad function can also be called a padStart, it takes the preferred padding and length character as arguments.

```
console.log(String(6).padStart(3, "0"));
// → 006
```

You can break a string on every development of another string with split and then join them together with join.

```
let sentence = "Secretarybirds specialize in stomping";
let words = sentence.split(" ");
console.log(words);
// → ["Secretarybirds", "specialize", "in", "stomping"]
console.log(words.join(" "));
// → Secretarybirds. specialize. in. stomping
```

You can use the repeat method to repeat a string, which develops a new string holding several copies of the original string attached together.

```
console.log("LA".repeat(3));
```