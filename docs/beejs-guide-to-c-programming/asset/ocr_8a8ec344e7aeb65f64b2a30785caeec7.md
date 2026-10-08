You can give them a tag name so you can refer to the type later and declare variables of that type.

Now, since enums are integer types, why not just use int?

In C, the best reason for this is code clarity-it's a nice, typed to describe your thinking in code. C (unlike C++) doesn't actually enforce any values in range for a particular enum.

Let's do an example where we declare a r of type enum resource that can hold those values:

```
// Named enum, type is "enum resource"

enum resource {
  SHEEP,
  WHEAT,
  WOOD,
  BRICK,
  ORE
};
```

// Declare a variable "r" of type "enum resource"

```
enum resource r = BRICK;

if (r == BRICK) {
  printf("I'll trade you a brick for two sheep.\n")
}
```

You can also typedef these, of course, though I personally don't like to.

```
typedef enum {
  SHEEP,
  WHEAT,
  WOOD,
  BRICK,
  ORE
} RESOURCE;
```

RESOURCE r = BRICK;

Another shortcut that's legal but rare to declare variables when you declare the enum:

// Declare an enum and some initialized variables of that type:

```
enum {
  SHEEP,
  WHEAT,
  WOOD,
  BRICK,
  ORE
} r = BRICK, s = WOOD;
```

You can also give the enum name so you can use it later, which is probably what you want to do in most cases.

// Declare an enum and some initialized variables of that type:

```
enum resource {
// <-- type is now "enum resource"
  SHEEP,
  WHEAT,
```