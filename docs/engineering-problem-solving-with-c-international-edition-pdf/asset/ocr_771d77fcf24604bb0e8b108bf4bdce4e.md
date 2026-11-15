![](bbox=[0.22, 0.09, 0.86, 0.29])

Figure 6.20 Simulated wind speed.

+   31. Write a program to generate a data file named wind.dat that contains 1 hour of simulated wind speeds. Each line of the data file should contain the time in seconds and the corresponding wind speed. The time should start with 0 seconds. The increment in time should be 10 seconds and the final line of the data file should correspond to 3,600 seconds. The user should be prompted to enter the average wind speed and the range of values of the gusts.

+   32. In problem 31, assume that we want the flight simulator wind data to include a 0.5% possibility of encountering a small storm at each time step. Therefore, modify the solution to problem 31 so that the average wind speed is increased by 10 mph for a period of 5 minutes when a storm is encountered. A plot of an example data file with three storms is shown in Figure 6.21.

![](bbox=[0.22, 0.58, 0.86, 0.78])

Figure 6.21 Simulated wind speeds with three storms.

+   33. In problem 32, assume that there is a 1% possibility of encountering a microburst at each time step in a small storm. Therefore, modify the solution to problem 32 so that the wind speed is increased by 50 mph over the storm values for a period of 1 minute if a microburst is encountered. A plot of a sample data file with a microburst within a storm is shown in Figure 6.22.