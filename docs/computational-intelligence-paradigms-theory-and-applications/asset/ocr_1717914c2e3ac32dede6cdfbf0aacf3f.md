their alpha-cuts are

aA = [2a-1, 3-2a]
aB = [2a+1, 5-2a]

Using the operations definitions, we obtain

a(A+B) = [4a, 8-4a] for a in [0,1]
a(A-B) = [4a-6, 2-4a] for a in [0,1]
a(A*B) = [-4a^2+12a-5, 4a^2-16a+15] for a in [0,0.5]
         [4a^2-1, 4a^2-16a+15] for a in [0.5,1]
a(A/B) = [(2a-1)/(2a+1), (3-2a)/(2a+1)] for a in [0,0.5]
         [(2a-1)/(5-2a), (3-2a)/(2a+1)] for a in [0.5,1]

The resulting fuzzy numbers are then:

(A+B)(x) = 
{ 0,          for x ≤ 0 and x > 8
  x/4,        for 0 < x ≤ 4
  (8-x)/4,    for 4 < x ≤ 8 }

(A-B)(x) = 
{ 0,          for x ≤ -6 and x > 2
  (x+6)/4,    for -6 < x ≤ -2
  (2-x)/4,    for -2 < x ≤ 2 }

(A*B)(x) = 
{ 0,                    for x < -5 and x ≥ 2
  [3 - sqrt(4 - x)]/2,  for -5 ≤ x < 0
  [sqrt(1 - x)/2],      for 0 ≤ x < 3
  [4 - sqrt(1 + x)]/2,  for 3 ≤ x < 15 }

(A/B)(x) = 
{ 0,                for x < -1 and x ≥ 2
  (x+1)/(2-2x),     for -1 ≤ x < 0
  (5x+1)/(2x+2),    for 0 ≤ x < 1/3
  (3-x)/(2x+2),     for 1/3 ≤ x < 3 }

Another technique for developing fuzzy arithmetic based on the extension principle is one in which standard arithmetic operations on real numbers are extended to fuzzy number

(A#B)(z) = supremum(z=x#y) min[A(x),B(y)]

for all z in the set of real numbers. More specifically, we define for all z in R:

(A+B)(z) = supremum(z=x+y) min[A(x),B(y)]
(A-B)(z) = supremum(z=x-y) min[A(x),B(y)]
(A*B)(z) = supremum(z=x*y) min[A(x),B(y)]
(A/B)(z) = supremum(z=x/y) min[A(x),B(y)]