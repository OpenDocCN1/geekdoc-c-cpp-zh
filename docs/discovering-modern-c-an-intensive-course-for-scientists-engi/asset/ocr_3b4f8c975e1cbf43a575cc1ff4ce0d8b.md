# ## 4.8.2 STL Container

Create a `std::map` for phone numbers; i.e., map from a string to an unsigned `long`. Fill the map with at least four entries. Search for an existing and a non-existing name. Also search for an existing and a non-existing number.

# ## 4.8.3 Complex Numbers

Implement a visualization of the Julia set (of a quadratic polynomial) similar to the Mandelbrot set. The mere difference is that the constant added to the square function is independent of the pixel position. Essentially, you have to introduce a constant `k` and modify `iterate` a little.

+   - Start with `k = -0.6 + 0.6i` (Figure 4-9) which is a complex Cantor dust, also known as Fatou dust.
+   - Try other values for `k`, like `0.353 + 0.288i` (compare `http://warp.povusers.org/Mandelbrot/`). Eventually you may want to change the color scheme to come up with a cooler visualization.
+   - The challenge in software design is to write an implementation for both Mandelbrot and Julia sets with minimal code redundancy. (The algorithmic challenge is probably finding colors that look good for all `k`. But this goes beyond the scope of this book.)

![](bbox=[0.23, 0.54, 0.81, 0.85])

Figure 4-9: Julia set for `k == -0.6 + 0.6i` yielding a complex Cantor dust