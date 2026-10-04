```
// Prompt the user for the mass and velocity of the object
std::cout << "Enter the mass of the object (in kg): ";
std::cin >> mass;

std::cout << "Enter the velocity of the object (in m/s): ";
std::cin >> velocity;

// Calculate the kinetic energy
double kinetic_energy = (mass * std::pow(velocity, 2)) / 2;

// Display the result
std::cout << "The kinetic energy of the object is: " << kinetic_energy << " Joules" << std::endl;

return 0;
}
```