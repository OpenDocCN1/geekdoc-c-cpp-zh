![](bbox=[0.05, 0.05, 0.92, 0.25])

Fig. 6.25. Paths of a particle not captured within the magnetic field

Fig. 6.26. Particle captured in the magnetic field

The results shown in figures 6.25 and 6.26 were obtained with the analog computer set to repetitive operation with an OP-time of 10 ms and time scale factors k0 = 10³ set on all four integrators.

Figure 6.25 shows two typical paths of a particle which is deflected by the magnetic field but not captured. The values for α and β were the same for both pictures. Only x2, the coordinate at which the magnetic field ceases to act on the right side, has been increased in the second case. The particle in the left picture is fast enough to escape the narrow magnetic field while the wider field in the right picture causes the particle to be reflected.

Figure 6.26 shows the path of a particle with heavy friction. The friction is so large that the particle cannot escape the area in which the magnetic field acts.

# 6.8 Rutherford-scattering

In the early 20th century ERNEST RUTHERFORD performed a seminal experiment in which he bombarded a thin gold foil with α-particles.⁸⁹ He observed that the vast majority of these particles just went through the gold foil without being deflected or absorbed. Nevertheless, some of these particles were deflected through large angles with even fewer α-particles being reflected by the gold foil, a phenomenon called RUTHERFORD-scattering. This led to the planetary RUTHERFORD model of the atom, which then became the basis of the BOHR model.

The following analog computer simulation was motivated by [BORCHARDT]. It is assumed that the gold atom's nucleus is at a fixed position – specifically the point of origin of the underlying coordinate system to simplify the distance calculation for the α-particle. With the α-particle's position being (x, y) its distance to the gold nucleus is then

$r^2 = x^2 + y^2.$

89 These are Helium nuclei and thus rather large.