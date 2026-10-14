Coordinate type
    boxing, 115–116
    value type memory layout, 71–72
    value tuples, 102–103
copying, 46–48, 105–137
    copy-by-value semantics, 73–74
    defensive copies, 128–133
    identifying unnecessary boxing, 115–118
    large instances, 272
    locks and reference semantics, 46–47
    measuring cost of, 270–271
    method parameters and
        arguments, 118–123
    modifying return type instances, 123–128
    new object creation, 110–115
    references vs. instances, 105–106
    simple assignment, 106–110
    value equality, 47–48
    value semantics vs. reference semantics, 177–181
CPU sampling, 254, 271
CreateColor method, returning by reference and, 100
CrossGen utility, 250
D
dammit (!; null-forgiving) operator, 66–67
dangling references, 84, 99
DataAdapter type, generic type constraints and, 234–238
DataStore type, reference semantics and, 74–75
DateTime type
    boxing, 118
    IComparable interface, 206
    TryXXX idiom, 79–80
decimal type, 143
declaration patterns, 150, 157
declarative code
    defined, 89
    immutability, 89
    performance and, 91–92
    vs. procedural code, 89, 284
Deconstruct method, 102–103
deep copies (clones), 200
default constructor, 52–54, 58
default keyword, 62–63
default values
    avoiding pitfalls of default variables, 200–201
    default initialization, 50, 56
    generics and, 62–63
    null, 64
    object initializers, 59
    valid, 63
defensive copies, 128–133
    automatic vs. nonautomatic properties, 130–131
    avoiding, 133–136
    causes of, 133
    defending against mutation, 133–134, 136
    mutable value types and in parameters, 129–130
    read-only fields, 132–133
    read-only reference variables, 131–132
definite assignment, 39
    generics, 62
    ref and out parameters, 79
    static fields, 58
    struct variables, 56–57
deferred execution (lazy enumeration), 85
delegates
    callback delegate, 93–94
    defined, 93, 241
    generic, for polymorphism, 241–242
derived type, 34
Difference method, memory layout of method parameters and, 72
digit separators, 262
Direction property, nondestructive mutation and, 90–91, 127–128
discard pattern, 20–21, 195, 284–285
Disconnect method, reference semantics and, 178–179, 181
disjunctive pattern, 195
Displacement method, 2–29
    custom types, 5–6
    encoding units, 18–28