A possibly more interesting use case is when we wish to display one or more vectors as line graphs as a way to visualise them. This is the subject of the next section.

# 14.5.1 Single and Multiple Curves

We have two functions to display vectors. The first function displays a list of vectors while the second function displays a single vector. The interfaces are:

```
// Create chart with a number of functions. The arguments are:
// x:              std::vector<double> with input values
// labels:         labels for output values
// vectorList:     list of vectors with output values.
// chartTitle:     title of chart
// xTitle:         label of x axis
// yTitle:         label of y axis
void CreateChart(const std::vector<double> & x,
                const std::list<std::string> & labels,
                const std::list<std::vector<double>> & vectorList,
                const std::string& chartTitle,
                const std::string& xTitle = "X",
                const std::string& yTitle = "Y");
```

```
// Create chart with a number of functions. The arguments are:
// x:              std::vector<double> with input values
// y:              std::vector<double> with output values.
// chartTitle:     title of chart
// xTitle:         label of x axis
// yTitle:         label of y axis

void CreateChart(const std::vector<double> & x,
                const std::vector<double>& y,
                const std::string& chartTitle,
                const std::string& xTitle = "X",
                const std::string& yTitle = "Y");
```

Using these functions is similar to the approach taken in Section 14.4. We initially consider the case of the function f(x) = x². Note that it is convenient to define it as a stored lambda function fun:

```
long N = 40;

// Create abscissa x array
double A = 0.0; double B = 10.0;
auto x = CreateMesh(N, A,B);

auto fun = [](double x) { return x*x; };
auto vec1 = CreateDiscreteFunction< std::vector<double>>(x, fun);

ExcelDriver xl; xl.MakeVisible(true);
xl.CreateChart(x, vec1, "Test 101 curve");
```