Answer: (a) Even this works right. The necessity of 'virtual' is only on hierarchical inheritance part.

# 106. What is the output of the code? (L4)

```
#include<iostream>
using namespace std;
class base
{ };
class dev1 : public base
{ }S;
class dev2 : public dev1
{ }D;
class dev3 : public dev1
{ }E;
class dev4 : public dev2, public dev3
{ }F;
int main()
{ cout<<"fun"; }
```

+   (a) fun
+   (b) Prints nothing
+   (c) Error
+   (d) None of the above

Answer: (a) When both the base classes is empty there is no chance of collision and 'virtual' keyword can be skipped. But it has no significance.

# 107. What is the type of inheritance used? (L3)

```
#include<iostream>
using namespace std;
class base
{ //block A;
  class dev1 : public base
  { //block }S;
  class dev2 : public dev1
  { //block }D;
  class dev3 : public dev1
  { //block }E;
  class dev4 : public dev2, public dev3
  { //block }F;
```

```
class dev5 : public dev4
{ //block }V;
  int main()
  { //block }
```

+   (a) Hybrid
+   (b) Hierarchical
+   (c) Multilevel
+   (d) Multiple

Answer: (a) It is a combination of simple, multilevel and hierarchical modes.

# 108. What is the type of inheritance used? (L3)

```
#include<iostream>
using namespace std;
class base
{ //block }A;
  class dev1 : public base
  { //block }S;
  class dev2 : public dev1
  { //block }D;
  class dev3 : public dev2
  { //block }E;
  class dev4 : public dev3
  { //block }F;
  class dev5 : public dev3
  { //block }V;
  int main()
  { //block }
```

+   (a) Hybrid
+   (b) Hierarchical
+   (c) Multilevel
+   (d) Multiple

Answer: (a) It has multilevel followed by hierarchical.

# 109. What is the type of inheritance used? (L5)

```
#include<iostream>
using namespace std;
class base
{ //block }A;
  class dev1 : public base
  { //block }S;
  class dev2 : public dev1
```