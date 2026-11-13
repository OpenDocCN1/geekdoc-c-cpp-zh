# Choice of Hash Function

The choice of the hash function is a very difficult job in hashing. It is not possible for selecting a perfect hash function, which is suitable for all different kinds of problem. There may be three possible ways to choose a hash function.

+   - Perfect Hash Function: There is no feasibility of this type of hash function if the data is large because practically it is not possible for huge data.
+   - Desirable Hash Function: For these hash function the address space should be small and collision should be kept very less or minimum.

# Criteria of Hash Function

The two main criteria used in selecting a hash function are:

+   - Function H should be very easy and quick to compute.
+   - The function H should be as far as possible uniformly distribute the hash address throughout the set L. So, there is a minimum number of the collision.

Typical Hash functions are as follows:

# Division method

Division method is the simplest and most common way of implementing a hash function for a large volume of data. The aim of this function is to compute the index of a hash table.

The hash function H is defined by
H (K) = K mod m, [generates index value from 0 to m-1]
or
H (K) = (K mod m) + 1, [generates index value from 1 to m]

The number m is usually chosen to be a prime number (since this frequently minimizes the number of collisions). Here, the first function denotes the remainder when k is divided by m. The second function is used if the hash address ranges from 1 to m rather than from 0 to m-1.

# Example:

Suppose key values are 3205, 7148, 2345 and table size 100. Select M = 97 is a prime number
H (3205) = 3205 mod 97 = 4
H (7148) = 7148 mod 97 = 67
H (2345) = 2345 mod 97 = 17

# Mid squares method

In mid square method, the key is multiplied by itself (i.e. k^2) and select a number of digits from the middle of the result. How many digits you select will depend on your table size and the size of your hash key. If the square is considered as the decimal number, the table size must be a power of 10. The mid square method squares the key value and then takes out the middle digits of the square result.

# Example:

| K: | 3205 | 7148 | 2345 |
|---|---|---|---|
| K^2: | 10272025 | 51093904 | 5499025 |
| H(K): | 72 | 93 | 99 |