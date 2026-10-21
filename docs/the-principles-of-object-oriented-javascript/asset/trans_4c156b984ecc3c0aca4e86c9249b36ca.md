
constructors (continued)
stealing, 75–76
subtype, 72, 75–76
supertype, 72, 75–76
create() method, 70
creating
accessor properties, 42–43
objects, 6–7
properties, on temporary objects, 15
Crockford, Douglas, 69

## D
data
sharing private, 83–84
storing on prototype, 57
types. See primitive types; reference types; types
data properties, 37
attributes, 40–41
from mixins, 88–89
Date built-in type, 8
Date object, valueOf() method, 67
declarations, vs. expressions, 18–19
defineProperties() method, 43–44
defineProperty() method, 39–41, 52
[[Delete]] operation, for object property, 35
delete operator, 35, 48
dereferencing, objects, 7–8
detecting properties, 33–35
dot notation, for property access, 11
double equals operator (==), 5
double-square-bracket notation ([[ ]]), 17

## E
enumerable properties
adding to Object.prototype, 69
copying between supplier and receiver, 84
[[Enumerable]] property attribute, 39, 42
enumeration, 36–37
equals operators, double (==) and triple (===), 5
Error built-in type, 9
errors
from constructors in strict mode, 53
for primitive wrapper objects, 16
event support, adding to objects, 85–87
expressions, vs. declarations, 18–19

[[Extensible]] attribute, 45–47
extensions for objects, preventing, 45

## F
falsy values, 33
first-class functions, 2
flexibility of JavaScript, 2
for-in loops, 36, 69, 84
frames of web pages, passing values between, 13
freeze() method, 47, 61
freezing objects, 47
frozen objects, prototype modification and, 61
Function constructor, 9, 10, 20
function keyword, 18
function literals, 10–11
functions, 2, 17–29
declarations vs. expressions, 18–19
hoisting, 18–19
overloading, 23–24
parameters, 21–22
as values, 19–21

## G
garbage-collection language, JavaScript as, 7
[[Get]] attribute, 41
getOwnPropertyDescriptor() method, 44
getPrototypeOf() method, 55
getter functions, 37–38
global object, this to represent, 25

## H
hash maps, JavaScript objects as, 48
hasOwnProperty() method, 34–35, 53, 66, 69
hoisting functions, 18–19

## I
if condition, 33
immediately invoked function expression (IIFE), 80
inheritance, 65–78
constructor, 72–75
methods from Object.prototype, 66–68
between objects, 69–72
prototype chaining, 65–69
pseudoclassical, 76, 87

in operator, 53
testing for property instance with, 33–34
instanceof operator, 12–13
temporary objects and, 15
instances. See also objects
checking type of, 50–51
prototype link to constructor, 60
of reference types, 6
instantiating
built-in types, 8–11
objects, 6
primitive wrappers, 16
internal property, of functions, 17
isArray() method, 13–14
isExtensible() method, 45, 46
isFrozen() method, 47
isPrototypeOf() method, 55, 66
isSealed() method, 46

## K
keys() method, 36, 89–90
key/value pairs, 48

## L
length property, of functions, 21–22
literals, 3, 9
array, 10
function, 10–11
object, 9–10
regular expression, 11

## M
memory location, pointer to, 7
methods, 6, 24–28
adding to arrays, 62
primitive, 6
privileged, 80
prototypes for defining, 57–60
for supertypes, accessing, 77
mixins, 84–90
data properties from, 88–89
module patterns, 80–82

## N
names
for constructors, capitalization of, 50
multiple functions with same, 23
for properties, 80
new operator, 6, 90–92
constructors and, 49, 50, 52
instantiating reference types with, 9
this object created with, 51
null value, 3
determining if a value is, 5
setting object variable to, 7–8
setting property to, 35
typeof operator and, 5
Number primitive wrapper type, 14–15
number type, 3

## O
Object built-in type, 9
Object constructor, 32
Object.create() method, 70
Object.defineProperties() method, 43–44
Object.defineProperty() method, 39–41, 52
Object.freeze() method, 47, 61
Object.getOwnPropertyDescriptor() method, 44
Object.getPrototypeOf() method, 55
Object.isExtensible() method, 45, 46
Object.isFrozen() method, 47
Object.isSealed() method, 46
Object.keys() method, 36, 89–90
object literals, 9–10
object patterns, 79–92
private and privileged members, 80–84
Object.preventExtensions() method, 45
Object.prototype.isPrototypeOf() method, 55, 66
Object.prototype prototype
methods inherited from, 66–68
modifying, 68–69
objects, 2, 6, 31–48
creating, 6–7
dereferencing, 7–8
freezing, 47
inheritance, 69–72
methods, 24–28
modification, preventing, 45–47
properties, defining, 32–33
property inheritance from prototype, 65–69
reference types as, 2
sealing, 45–46
Object.seal() method, 45–46, 61
overloading functions, 23–24

## P
own properties
determining existence of, 66
determining whether enumerable, 66
in operator to check for, 34
for objects, 32
vs. prototype properties, 55–56

parameters, 21–22
person object, module pattern for creating, 81
pointer to memory location, 7
preventExtensions() method, 45
preventing object modifications, 45–47
primitive methods, 6
primitive types, 2, 3–6
primitive wrapper types, 14–16
private data, sharing, 83–84
private members, 80–84
for constructors, 82–84
privileged members, 80–84
properties, 6, 11–12, 80
adding or removing, 8
copying enumerable, between receiver and supplier, 84–86
creating on temporary objects, 15
defining, 32–33
defining multiple, 43–44
detecting, 33–35
enumerable, adding to Object.prototype, 69
enumeration, 36–37
identifying on prototype, 54
removing, 35
string literals for names, 9
types, 37–38
property attributes, 38–44
changing, 39–40
retrieving, 44
propertyIsEnumerable() method, 37, 39, 66
_proto_ property, 55
prototype chaining, 65–69, 71, 74
object without, 72
overwriting, 73
prototype properties
identifying, 54
vs. own properties, 55–56
prototype property, of functions, 53, 72
[[Prototype]] property, 54–56, 60–61

prototypes, 53–63
built-in object, 62–63
changing, 60–62
identifying properties, 54
overwriting, 59
property inheritance from, 65–69
use with constructors, 57–60
pseudoclassical inheritance, 76, 87
pseudoinheritance, mixins for, 84
[[Put]] method, 32–33
for data properties, 37

## R
read-only property, 38
receiver, copying enumerable properties between supplier and, 84–86
Rectangle constructor, 73–75
reference types, 2, 6–8
identifying, 12–13
reference values, storing on prototype, 57–58
RegExp built-in type, 9
RegExp constructor, 11
regular expression literals, 11
removing properties, 8, 35
retrieving property attributes, 44
revealing module pattern, 82

## S
scope-safe constructors, 90–92
sealed objects, prototype modification and, 61
sealing objects, 45–46
seal() method, 45–46, 61
[[Set]] attribute, 32–33, 41
setter functions, 37–38
sharing private data, 83–84
signatures, function with multiple, 23
sort() method, 20
square brackets ([ ])
for array literals, 10
for property access, 11–12
Square constructor, 73–75
stealing constructors, 75–76
strict mode
for nonextensible objects, 45
for sealed objects, 46
string literals, as property names, 9
String primitive wrapper type, 14–15

strings
capitalize() method, 62
conversion of values to, for comparison, 21
methods, 6
string type, 3
substring() method, 6
subtype constructors, 72, 75–76
sum() function, 21
supertype
constructors, 72, 75–76
methods, accessing, 77
supplier, copying enumerable properties between receiver and, 84–86

## T
temporary objects, creating properties on, 15
this object, 25–26
changing value of, 26–28
to create length and width properties, 76
creating with new, 51
toFixed() method, 6
toLowerCase() method, 6
toString() method, 6, 35, 66, 67–68
triple equals operator (===), 5
truthy values, 33
typeof operator, 4–5, 12
types, 2. See also primitive types; reference types
checking for different, 24
checking instance for, 50–51
instantiating built-in, 8–11

## U
undefined type, 3
underscore (_), in property name prefix, 38, 80

## V
[[Value]] attribute, 40
valueOf() method, 66, 67
values
functions as, 19–21
passing, between web page frames, 13
variable object, 2
variables, for primitive types, 3–4

## W
web pages, passing values between frames, 13
wrapper types, primitive, 14–16
[[Writable]] attribute, 40
write-only properties, 38
