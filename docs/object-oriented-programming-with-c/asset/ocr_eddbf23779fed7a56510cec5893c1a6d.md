Here, off is 0 and on is 1. These constants may be referenced in the same manner as regular constants. Examples:

+   int switch_1 = off;
+   int switch_2 = on;

In practice, enumeration is used to define symbolic constants for a switch statement. Example:

+   enum shape
+   { circle, rectangle, triangle
+   }; int main()
+   { cout << "Enter shape code:"; int code; cin >> code; while(code >= circle && code <= triangle)
+   { switch(code)
+   { case circle: ..... break; case rectangle: ..... break; case triangle: ..... break; } }