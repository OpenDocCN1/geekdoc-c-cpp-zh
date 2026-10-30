by the area of the trapezium with corners \((p,0)\), \((p,f(p))\), \((q,f(q))\), \((q,0)\). This area is simply \((f(p)+f(q))(q-p)/2\). Use this to compute the natural logarithm.

+   5. Simpson’s rule gives the following approximation of the area under the curve of a function \(f\):
+   
+   \[
+   \int_a^b f(x)\,dx \approx \frac{b-a}{6}\left(f(a)+4f\left(\frac{a+b}{2}\right)+f(b)\right)
+   \]
+   
+   Use this rule for each strip to get another way to find the natural log.

+   6. Suppose we are given \(n\) points in the plane: \((x_1,y_1),\ldots,(x_n,y_n)\). Suppose the points are the vertices of a polygon, and are given in the counterclockwise direction around the polygon. Write a program to calculate the area of the polygon. Hint 1: Break the area into small triangles with known coordinates. Then compute the lengths of the sides of the triangles, and then use Heron’s formula to find the area of the triangles. Then add up. Hint 2: Break the boundary of the polygon into two parts, an up facing boundary and a down facing boundary. Express the area as the area under these boundaries each considered as functions \(f(u)\).

+   7. Children often play a guessing game as follows. One child, Kashinath, picks a number between 1 and 1000 which he does not disclose to another child, Ashalata. Ashalata asks questions of the form “Is you number between \(x\) and \(y\)?” where she can pick \(x,y\) as she wants. Ashalata’s goal is to ask as few questions as possible and determine the number that Kashinath picked. Show that Ashalata can guess the number correctly using at most 10 questions. Hint: Use ideas from the bisection method.

+   8. Write a program to find \(\arcsin(x)\) given \(x\).

+   9. Consider a circuit in which a voltage source of \(V_{CC}=1.5\) volts is applied to a diode and a resistance of \(R=1\) Ohm connected in series, Figure 8.4. The current \(I\) through a diode across which there is a potential drop of \(V\) is
+   
+   \[
+   I=I_S(e^{V/(nV_T)}-1)
+   \]
+   
+   where \(I_S\) is the reverse saturation current of the diode, \(V_T\) is the thermal voltage which is about 25 mV at room temperature (300 Kelvin), and \(n\) is the ideality factor. Suppose the diode we are using has \(n=1\) and \(I_S=30\) mA. Write a program that finds the current. Use your program to also find the current when the voltage source is reversed.

+   10. Consider the problem of finding the roots of \(f(x)=x^3-x/2+1/4\). See what happens using the Newton-Raphson method for the guesses for the initial value. In particular, try \(x_0=1\) and \(x_0=0.5\). Can you solve this using the bisection method?