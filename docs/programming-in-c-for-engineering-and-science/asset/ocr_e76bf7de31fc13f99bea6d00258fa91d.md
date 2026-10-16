The program in Example 7.3 inputs the resistance, inductance, capacitance, the frequency of the a-c source, and the voltage, and then uses the preceding equations to calculate the current and output it.

# Example 7.3 Current in an A-C Circuit

```
/* This program computes the current in an a-c circuit containing a capacitor, an inductor, and a resistor in series.

Input: resistance, inductance, capacitance, frequency, voltage
Output: current
*/

#include <iostream>  // cin, cout, <<, >>
#include <complex>  // complex<double> type
#include <iomanip>  // format output
using namespace std;

int main()
{
  const complex<double> i = complex<double>(0, 1);
  double R,  // resistance (ohms)
  L,  // inductance (henrys)
  C,  // capacitance (farads)
  omega;  // frequency (radians per second)
  complex<double> V,  // voltage (volts)
  Z,  // total impedance
  I;  // current (amperes)
  cout << "\nEnter resistance (ohms), inductance (henrys),\n and capacitance (farads): ";
  cin >> R >> L >> C;
  cout << "\nEnter frequency (radians/second): ";
  cin >> omega;
  cout << "\nEnter voltage as a complex number in the form (x, y): ";
  cin >> V;
  // Calculate resistance using complex arithmetic
  Z = R + omega * L * i - i / (omega * C);
  // Calculate and display current using complex arithmetic
  I = V / Z;
  cout << fixed << setprecision(2)
       << "\nCurrent = " << real(I) << " + " << imag(I) << "I"
       << "\nwith magnitude = " << abs(I) << endl;
}
```