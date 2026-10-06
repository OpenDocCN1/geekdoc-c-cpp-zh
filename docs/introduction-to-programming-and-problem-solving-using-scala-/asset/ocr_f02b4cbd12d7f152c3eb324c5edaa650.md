# Introduction to Programming and Problem-Solving Using Scala

8. Kyle is hungry for pizza and wants to get the best pizza deal. He is not sure if it is better to get two cheaper medium sized pizzas or one large pizza. Write a script that will help him figure out which to order. He can get two 12 inch pizzas for $12.00 or 14 inch pizza for $9. Hint: Use the formula $\pi r^2$ to find the area of a pizza in inches.

9. Bryn just started a new job, but is already thinking of retirement. She wants to retire as a millionaire. She plans on saving $700 per month and expects to receive an annual return of 7%. Will she be a millionaire if she retires in 30 years? Write a script to figure this out.

10. A town administrator in west Texas is trying to decide if she should build a larger water tower. The town has a water tower that contains 20,000 gallons of water. If there is no rain, write a script that will calculate the number of weeks the water will last based on the town's usage (provided by the town administrator). The weekly usage does not exceed 20,000 gallons.

11. Write a script that will calculate how a projectile will go given a launch speed and angle of friction. Assume that the projectile is launched from ground with a certain speed in m/s and angle in radians. Use the fact that acceleration due to gravity is $9.8m/s^2$. The steps in doing this would be to calculate the speed parallel and perpendicular to the ground with math.sin and math.cos, figure out how long the projectile to slow to a vertical speed of zero ($v = v_0 - at$), and use that to determine how long it stays in the air.

12. Quinn is planning on seeding a lawn of about 1500 square feet in her backyard this spring and wants to know how much soil and grass seed she needs. She lives in a new development and is pretty barren and rocky in the backyard; so she must plan down 6 inches of top. Most grass seed recommend 4 to 5 lbs. of grass seed for each 1,000 square foot of land for calculating grass seed. How many cubic yards of top soil and how pounds of grass seed does she need to buy? Write a script to help her find the answer.

13. Using Scala as a calculator, figure out how much you have to make each year to bring home $100,000 assuming a 27% tax rate.

14. In the REPL, declare a variable with the type String that has the name string. On the next line, then hit tab to see the methods for String. By playing around the REPL try to figure out what the methods do.

+   - toUpperCase
- trim
- substring — This method takes two Int arguments.
- replace — This method can be called with two Char or String arguments.

15. Kepler's third law of planetary motion says that $P^2 \propto a^3$, where $P$ is the orbital period, and $a$ is the semi-major axis of the orbit. For our Sun, if $P$ in years and $a$ in Astronomical Units (AU), the proportionality becomes equals. Look up the semi-major axis values for three bodies in our solar system other than the Earth and use Scala as a calculator to find the period according to Kepler's third law.