# Recipe 1: Execute Exception Safety Technique

# Situation

When an error occurs in C++, the code should keep running properly without wasting resources or corrupting data. This is called exception safety. This is quite important in "GitforGits," particularly in the sections of the program that handle file operations, communication over networks, or complicated data processing. Finding the sweet spot between performance, readability, and exception safety is no easy feat. Resource Acquisition Is Initialization (RAII), smart pointers, and transactional design patterns are a few of the techniques that C++ offers to make this possible.

# Practical Solution

# Levels of Exception Safety

Basic Guarantee: At a minimum, ensure that invariants of components are preserved, and no resources are leaked. This often involves using smart pointers to manage resources automatically.

Strong Guarantee: This level aims to make operations atomic; they either complete successfully or have no effect at all, rolling back to the