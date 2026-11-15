rand_float prototype statement:
a, b
rand_float function:
a, b
3. external identifiers: none
4. local variables and scope:
main function:
n, k, a0, a1, a2, a3, a, b, step, left, right
check_roots prototype statement:
left, right, a0, a1, a2, a3
check_roots function:
left, right, a0, a1, a2, a3, f_left, f_right
poly prototype statement:
x, a0, a1, a2, a3
poly function:
x, a0, a1, a2, a3

# SECTION 4.9, PAGE 198

+   1. #define area_sq(side) ((side)*(side))
+   printf("area: %f \n",area_sq(side1));
+   2. #define area_rect(side1,side2) ((side1)*(side2))
+   sum = area_rect(side1,sideb) + area_rect(sidec,sided);
+   3. #define area_par(base,height) ((base)*(height))
+   area1 = area_par(b,hl);
+   4. #define area_trap(base,height1,height2)
+   (0.5*(base)*((height1)+(height2)))
+   area += area_trap(base,left,right);
+   5. #define vol_sph(radius) (4.0/3.0*3.14159*pow((radius),3))
+   printf("volume: %f \n",vol_sph(5.5);
+   6. #define vol_pyr(area,height) ((1.0/3.0)*(area)*(height))
+   vol1 = vol_pyr(0.5*baseb*baseht,pyhrt);
+   7. #define vol_cone(radius,height)
+   (1.0/3.0*3.141593*pow((radius),3)*(height))
+   vol2 = vol_cone(diameter/2,ht);
+   8. #define vol_cube(side) ((side)*(side)*(side))
+   vol3 = vol_cube(sqrt(base,area));
+   9. #define vol_par(length,width,height)
+   ((length)*(width)*(height))
+   vol14 = vol_par(side1,side1,side1);