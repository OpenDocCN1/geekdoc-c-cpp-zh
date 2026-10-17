

## Figure 8.1 A hash is an associative container.

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_200_0.png)

A hash constitutes an associative container because it does not necessarily store the elements it contains using a logic based on the sequence of the indexes. Instead, you access the elements in a hash according to an order that the content of the elements establishes. The order the content establishes creates a situation in which association among the elements, rather than sequence, characterizes the logic that characterizes the container.

The elements in a hash can be said to be organized according to hashed keys. When you place a key in a hash, as Figure 8.1 indicates, you see a recognizable word. However, when you insert this word into the hash, the hash transforms (or hashes) it to make it so that it can serve, in essence, as a kind of encrypted index. This index might be placed in the container in any number of positions. An algorithm embedded in the programming behind the container determines this position. Given an effective design of the algorithm, when you search a hash for a given key, the hash retrieves the item more quickly than it could using a sequential search (which is the approach often employed with arrays).

Each key serves as a hashed index to a value. Perl hashes provide unique keys. When a hash provides unique keys, if it finds that you are inserting a key that the hash already contains, it replaces the old key with the new one. In Figure 8.2, when you insert the second and third elements with the key of `Alkali`, the third key displaces the first two, and when you examine the contents of the hash afterward, you find only the third entry, which in this case is associated with Potassium. The same form of displacement characterized the two Metalloid keys. In the end, you find only the key associated with Silicon.

| Category | Element |
|---|---|
| Noble Gasses | Helium |
| Alkali Metals | Lithium |
| Alkali Metals | Sodium |
| Alkali Metals | Potassium |
| Transition Metals | Titanium |
| Metalloids | Boron |
| Metalloids | Silicon |

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_201_0.png)

| Category | Element |
|---|---|
| Noble Gasses | Helium |
| Alkali Metals | Potassium |
| Transition Metals | Titanium |
| Metalloids | Silicon |

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_201_1.png)

What pertains to keys, however, does not pertain to values. As Figure 8.3 illustrates, as long as you insert unique keys, a hash stores multiple identical values.

| Key | Value |
|---|---|
| Helium | Noble Gasses |
| Lithium | Alkali Metals |
| Sodium | Alkali Metals |
| Potassium | Alkali Metals |
| Titanium | Transition Metals |
| Boron | Metalloids |
| Silicon | Metalloids |

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_201_2.png)

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_201_3.png)

The order in which the hash replaces duplicated keys is predictable. The most recently entered duplicate key displaces the older key. As for the organization of values in a hash, the situation depends on the algorithm behind the hash. When you display the items in a hash, it is difficult to predict the order of display. Consider the elements shown in Figure 8.3. This could be the order in which you see elements as you print them from a hash. The order of elements is not alphabetical. Nor is it the order in which you add values to the hash.

# Identifying and Initializing Hashes

Hashes have two contexts of use. One context is the implicit context. The other is the scalar context. When a hash appears in an implicit hash context, you identify it with a percent sign (%).

# CHAPTER 8 Hashes

When you use a hash in a scalar context, you identify it with a dollar sign ($). Listing08_01 shows you hashes initialized in both implicit and scalar contexts. The program produces no output.

```
#Listing08_01

#1 Implicit initialization using the
# correspondence operator (=>)
#Parentheses
%Elements = (Hydrogen => H,
             Helium => He,
             Manganese => Mn);

#Implicit initialization using a list
%Elements = ("Oxygen" , "O",
             "Nitrogen" , "N",
             "Potassium" , "K");

#2 Scalar initialization using
#Curly braces
        # correspondence operator (=>)
$Elements{Carbon}=C;
$Elements{Calcium}=C;
$Elements{Aluminum}=Al;
```

At comment #1 you first initialize a hash using the correspondence operator. To effect such an initialization, you prefix the percent sign to the hash identifier (%Elements). This designates an implicit hash. You then use a list operation (parentheses enclosing the keys and values) to designate the key-value pairs you want to assign to the hash. If you do not use the parentheses, the initialization will still work, but only for the first element (Hydrogen). The second form of implicit initialization using a list involves using commas rather than the correspondence operator. This approach works just as well as the first.

The lines associated with comment #2 allow you to continue the work of initializing the %Elements hash using the scalar, or lookup, form of initialization. In this case, you prefix a dollar sign to the hash identifier ($Elements) and employ curly braces ({ }) to enclose the key you want to designate. You then follow with an assignment operator and the value you want to associate with the key.

# Order of Initialization

When you initialize hashes using implicit and lookup forms of the hashes, you follow implicit form with the lookup form. Consider the following order of initialization:

```
#1 Lookup following implicit form works
%Elements = (Hydrogen =>  H);  #implicit
$Elements{Aluminum} = Al;       #lookup
```

When the lookup follows the implicit form, you see the following output if you print the contents of @Elements with formatting:

```
Aluminum Al
Hydrogen H
```

The Perl interpreter allows you to initialize a hash implicitly and then to add more elements to the hash with the scalar or lookup statement. You add Aluminum after Hydrogen, and when you print the contents, you see both elements.

This situation changes when you reverse the order. If you begin with a lookup form of initialization and then follow with an implicit form of initialization, the Perl interpreter does not add elements to your hash. Instead, it allows the implicit initialization to cancel the contents previously assigned. Consider initializations in the following lines:

```
#2 Implicit following lookup does not work
$Elements{"Calcium"}=       "Ca";       #lookup
$Elements{Aluminum}=        "Al";       #lookup
%Elements = ("Oxygen", "O");           #implicit – cancels previous
```

When you follow the two scalar expression with the implicit initialization, if you print the contents of @Elements with formatting, you see only one element:

```
Oxygen O
```

With the implicit initialization, you lose the contents of the hash as previously defined.

> It might seem that the behavior of Perl is arbitrary when you consider the way that you go back and forth between the implicit (%) and (scalar) explicit ($) forms. One way to counter this notion involves remembering that when you use explicit ($) form, you are dealing with an item in the hash as a single scalar. When you use the implicit form (%), you are dealing with the item as a part of the whole hash structure. It is as though you have thrown a switch.

# Variations on Initialization

When you employ either the implicit form of initialization or the scalar (lookup) form of initialization for hashes, you can represent the data you are dealing with in a number of ways. Listing08_02 provides examples of several somewhat random approaches to data representation. The program produces no output.

```
#Listing08_02

#1 Implicit initialization -- variations

# Scalar
$TableElement = "Hydrogen";

# A scalar and interpolated and literal strings
%Elements = ($TableElement => "H",
             "Helium" => 'He',
             'Manganese' => "Mn");

#2 Initialization using the scalar
$Elements{"Carbon"} = "C";
$Elements{"Calcium"} = "Ca";
$Elements{Aluminum} = "Al";

#3 Keys and values consisting of more than one word
#requires quotes
$CompoundName = "Carbon Monoxide";
%Compounds = ($CompoundName       => "CO",
              q(Plumbous Oxide)   => 'PbO',
              qq(Copper Hydroxide) => "CuOH");
$Compounds{"Calcium Oxide"}      =     "CaO";
```

At comment #1 in Listing08_02 you first assign an interpolated string to a scalar ($TableElement). Then, in the implicit form of initialization that follows, you insert the scalar in the position in the list that designates the key for the first element. For the value for the first element, you follow the correspondence operator (=>) with an interpolated string containing a single character, H, which designates the abbreviation for Hydrogen in the Table of Elements.

After inserting an element for Hydrogen, when you initialize the elements immediately following it, you first use an interpolated string ("Helium") for a key and a character string

