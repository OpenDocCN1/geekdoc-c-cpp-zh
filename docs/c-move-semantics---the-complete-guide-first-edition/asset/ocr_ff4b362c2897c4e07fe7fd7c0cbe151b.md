# # Contents

+   **Preface** ........................................................ xi
+   - An Experiment ..................................................... xi
+   - Versions of This Book ............................................. xii
+   - Acknowledgments .................................................... xiii

+   **About This Book** ................................................ xv
+   - What You Should Know Before Reading This Book ..................... xv
+   - Overall Structure of the Book ..................................... xv
+   - How to Read This Book ............................................. xvi
+   - The Way I Implement ................................................ xvi
+   - The C++ Standards .................................................. xvii
+   - Example Code and Additional Information ........................... xviii
+   - Feedback ........................................................... xviii

# Part I: Basic Features of Move Semantics ................................ 1

# 1  The Power of Move Semantics ........................................... 3

+   - 1.1  Motivation for Move Semantics ...................................... 3
+     - 1.1.1  Example with C++03 (Before Move Semantics) ....................... 3
+     - 1.1.2  Example Since C++11 (Using Move Semantics) ...................... 11
+   - 1.2  Implementing Move Semantics ......................................... 18
+     - 1.2.1  Using the Copy Constructor ...................................... 19
+     - 1.2.2  Using the Move Constructor ...................................... 20
+   - 1.3  Copying as a Fallback ............................................... 21
+   - 1.4  Move Semantics for const Objects .................................... 22
+     - 1.4.1  const Return Values ............................................. 23