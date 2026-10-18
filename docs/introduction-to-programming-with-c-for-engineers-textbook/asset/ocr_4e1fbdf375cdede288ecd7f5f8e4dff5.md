```
```cpp
cout << "Your income is " << income << endl;
const double kIncomeTax = 19.0;              // 19%
cout << "After " << kIncomeTax << "% tax deduction you get: ";
cout << ( 1.0 - kIncomeTax / kPercentageDiv ) * income << endl;

return 0;
}
```
```

Given a total number of investment months *m* and a compounding period *t*, also in months, line [61] computes a number *i* of compounding periods. Then, on line [63], the final sum is computed, exactly as in Eq. (2.3). On lines [65–66], the computed values are displayed on the screen. Finally, on lines [69–73], our income and also income after tax deductions are computed and displayed.

# 2.5.3 Building and Running the Software

We can easily launch the previous code in one of the online C++ compiler platforms, as mentioned in Section 2.4.2. However, building an application that can be launched like any other program in our system is a more convenient option in this case. To build the *CompInterest* application for Linux, we can follow the steps presented in Section 2.4.5. But because the code in Listing 2.2 uses only standard C++ mechanisms, this software component is rather general. Hence, it could work on any platform if we had the tools to create and maintain multi-platform projects. For each software development environment, we can manually create a suitable project and build the application. However, considering the number of such platforms and operating systems, doing so would be tedious. Instead, we can use the *CMake* project generator. With its support, not only this but all future projects can be automatically generated to fit different development platforms and various operating systems. All we need to do is install this free tool and write the *CMakeList.txt* file, which contains commands that tell *CMake* what to do. (These are described in Appendix A.6.1.) Fortunately, a suitable *CMakeList.txt* file is attached to the example projects and can be downloaded with the other sources from GitHub (https://github.com/BogCyg/BookCpp). Also fortunately, all of our projects use an almost-identical *CMakeList.txt* file.

Having built the *CompInterest* application, to test it, let’s assume we have $1000, the annual investment rate is 2.7%, and we wish to invest our capital for four months. After launching *CompInterest*, our interest can be easily computed as follows:

```
```text
Enter the initial amount to invest:
1000
Enter the annual rate [% per 12 months]:
2.7
Compound frequency is a period in months between computing interest
(e.g. if 2 times a year, enter 6)
If you don't know, enter 12 for a yearly compound frequency.
Enter the compound frequency [months 1-72]:
4
Enter the investment time [months 1-100]:
4
Your balance before tax, after 4 months of investment is: 1009
Your income is 9
After 19% tax deduction you get: 7.29
```
```

The previous main function can act as a simple template for similar programs that read data, do some simple computations, and output the result. Also, this project can be used as a startup to build an application with a graphical user interface (GUI) for a mobile platform or as a web component. We will discuss some of these ideas later.