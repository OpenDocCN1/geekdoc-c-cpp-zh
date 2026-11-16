\(\mathbf{I}_{\text{box}} = \begin{bmatrix} \frac{1}{12}m(b^2+c^2) & 0 & 0 \\ 0 & \frac{1}{12}m(a^2+c^2) & 0 \\ 0 & 0 & \frac{1}{12}m(a^2+b^2) \end{bmatrix}\)

# Cylinder

The dimensions of a cylinder are described by its height \(h\) and the two semi-axis lengths \(a\) and \(b\) of its base, as shown in Figure 14.2. If the cylinder is circular, then \(a = b\).

![](bbox=[0.17, 0.32, 0.39, 0.55])

Figure 14.2: A cylinder.

The center of mass lies at the point (0,0,h/2), and the total mass of the cylinder is \(m = \pi \rho t a b h\). The moments of inertia are then given by the integrals

```
\(I_{11} = \rho \int_{-h/2}^{h/2} \int_{-b}^{b} \int_{-a\sqrt{1-y^2/b^2}}^{a\sqrt{1-y^2/b^2}} (y^2+z^2) dx dy dz = \pi \rho a b h \left( \frac{1}{4}b^2 + \frac{1}{12}h^2 \right),\)
\((14.20) \quad I_{22} = \rho \int_{-h/2}^{h/2} \int_{-b}^{b} \int_{-a\sqrt{1-y^2/b^2}}^{a\sqrt{1-y^2/b^2}} (x^2+z^2) dx dy dz = \pi \rho a b h \left( \frac{1}{4}a^2 + \frac{1}{12}h^2 \right),\)
\(I_{33} = \rho \int_{-h/2}^{h/2} \int_{-b}^{b} \int_{-a\sqrt{1-y^2/b^2}}^{a\sqrt{1-y^2/b^2}} (x^2+y^2) dx dy dz = \frac{\pi}{4} \rho a b h (a^2+b^2).\)
```