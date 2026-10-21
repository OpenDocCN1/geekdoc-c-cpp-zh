+   - Determine how many CBox objects of a given size can be packed in another CBox object of a given size. This is effectively division, so you could implement this by overloading the / operator.
+   - Determine the volume of space remaining in a CBox object after packing it with the maximum number of CBox objects of a given size.

I had better stop right there! There are undoubtedly other functions that would be very useful but, in the interest of saving trees, we’ll consider the set to be complete, apart from ancillaries such as accessing dimensions, for example.

# Implementing the CBox Class

You really need to consider the degree of error protection that you want to build into the CBox class. The basic class that you defined to illustrate various aspects of classes is a starting point, but you should also consider some points a little more deeply. The constructor is a little weak in that it doesn’t ensure that the dimensions for a CBox are valid so perhaps the first thing you should do is to ensure that you always have valid objects. You could redefine the basic class as follows to do this:

```
class CBox                                    // Class definition at global scope
{
    public:
        // Constructor definition
        CBox(double lv = 1.0, double wv = 1.0, double hv = 1.0)
        {
            lv = lv <= 0? 1.0: lv;                  // Ensure positive
            wv = wv <= 0? 1.0: wv;                  // dimensions for
            hv = hv <= 0? 1.0: hv;                  // the object

            m_Length = lv > wv? lv: wv;             // Ensure that
            m_Width  = wv < lv? wv: lv;             // length >= width
            m_Height = hv;
        }

        // Function to calculate the volume of a box
        double Volume() const
        {
            return m_Length*m_Width*m_Height;
        }

        // Function providing the length of a box
        double GetLength() const { return m_Length; }

        // Function providing the width of a box
        double GetWidth() const { return m_Width; }

        // Function providing the height of a box
        double GetHeight() const { return m_Height; }

    private:
        double m_Length;                           // Length of a box in inches
        double m_Width;                            // Width of a box in inches
        double m_Height;                           // Height of a box in inches
};
```