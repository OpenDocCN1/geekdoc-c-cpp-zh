\( F_q^4 = C_a \left[ \vec{n}_j \cdot \left( \vec{u}_a - \vec{v}_q \right) \right] \vec{n}_j \quad (4.3.8) \)

where \( C_a \) is the air viscosity constant, \( \vec{u}_a \) is a vector that defines the speed and direction of the air, \( \vec{v}_q \) is the speed of the particle \( P_q \) and \( \vec{n}_j \) is the normal vector of the particle \( P_q \). When the air speed vector \( \vec{u}_a \) is equal to 0, the air remains immobile and the previous expression can be considered as air friction. Many other forces that are applied over the cloth are categorized as external forces. Examples of such forces are: the resulting force when manipulating the cloth and the force produced when hanging the cloth from one corner.

# Dynamic System Approach

After obtaining the forces applied over the particles of the mesh, we can formulate a dynamic representation of the system. To accomplish this, the particles must follow *Newton's Second Law*, as shown in Equation 4.3.9.

\( \sum F_q = m_q a_q \quad (4.3.9) \)

where \( F_q \) represents the forces applied over each particle \( P_q \), \( m_q \) is the mass of the particle, and \( a_q = \dot{P}_q \) the acceleration. From Equation 4.3.5, for each particle of the mesh we can obtain the differential equations in Equation 4.3.10.

\(\left\{\begin{array}{l} \dot{p}_{ix} = \frac{1}{m_j} F_{ix} \\ \dot{p}_{iy} = \frac{1}{m_j} F_{iy} \qquad i=1,...,n \\ \dot{p}_{jz} = \frac{1}{m_j} F_{jz} \qquad j=1,...,m \end{array}\right. \quad (4.3.10)\)

The computational methods used to solve differential systems can also be employed to resolve the cloth dynamics problem [Volino00]. In this particular case, due to the use of elongation functions instead of elongation constants, time-step techniques are recommended for solving the previous equations. In most cases, forces will not increase much, but they may increase to oppose the effects of severe elongations. By using the *Runge-Kutta-Fehlberg* method of fourth-fifth order, good results can be obtained.

# Simulation

After presenting the model and the equations that describe the dynamic behavior of the mesh, we can outline the description of the cloth animation method (see Figure 4.3.8).