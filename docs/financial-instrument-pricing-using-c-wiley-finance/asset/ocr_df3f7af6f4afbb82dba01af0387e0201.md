```
dfdt[1] = 999.0 * (-std::sin(t) - std::cos(t));

}
};
```

You should check the code to ensure that the Jacobian has been calculated correctly!
To aid visualisation and debugging we also create an observer class to store the arrays of computed values that we can display in Excel:

```
class WriteOutput
{
private:

public:
    std::vector<value_type> tValues;
    std::vector<value_type> y1Values;
    std::vector<value_type> y2Values;
public:
    WriteOutput() : tValues(std::vector<value_type>()),
                    y1Values(std::vector<value_type>()),
                    y2Values(std::vector<value_type>()) {}

    void operator ()(const vector_type &x, const value_type t)
    {
        tValues.push_back(t);
        y1Values.push_back(x[0]);
        y2Values.push_back(x[1]);
    }

    const std::vector<value_type>& xAxis() const
    {
        return tValues;
    }

    const std::vector<value_type>& y1Axis() const
    {
        return y1Values;
    }

    const std::vector<value_type>& y2Axis() const
    {
        return y2Values;
    }
};
```

A test program is:

```
// Example based on Lambert "Numerical Methods for Ordinary
// Differential Equations" Wiley 1991. page 213
```