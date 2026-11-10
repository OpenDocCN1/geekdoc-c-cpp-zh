condition, it must be updated regularly and smoothly to keep up with the changing state of the flight vehicle. In such cases, a Sugeno fuzzy inference system is extremely well suited to the task of smoothly interpolating the linear gains that would be applied across the input space; it's a natural and efficient gain scheduler. Similarly, a Sugeno system is suited for modeling nonlinear systems by interpolating between multiple linear models.

# ### Advantages of the Sugeno Method

+   - It's computationally efficient.
+   - It works well with linear techniques (e.g., PID control).
+   - It works well with optimization and adaptive techniques.
+   - It has guaranteed continuity of the output surface.
+   - It's well-suited to mathematical analysis.

# ### 7.5.3 Conversion of Mamdani to Sugeno System

The MATLAB command-line function mam2sug can be used to convert a Mamdani system into a Sugeno system (not necessarily with a single output) with constant output membership functions. It uses the centroid associated with all of the output membership functions of the Mamdani system. The following Mamdani system mam21.fis is taken as the input.

```
    % mam21.fis $
    [System]
    Name = 'mam21'
    Type = 'mamdani'
    NumInputs = 1
    NumOutputs = 1
    NumRules = 4
    AndMethod = 'min'
    OrMethod = 'max'
    ImpMethod = 'min'
    AggMethod = 'max'
    DefuzzMethod = 'centroid'

    [Input1]
    Name = 'angle'
    Range = [-5 5]
```