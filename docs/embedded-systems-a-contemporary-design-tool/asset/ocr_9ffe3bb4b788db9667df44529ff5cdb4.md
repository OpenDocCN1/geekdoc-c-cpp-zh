![](bbox=[0.38, 0.08, 0.88, 0.49])

mainly VLSI class devices. Once again, we are going to have only limited visibility into the internals of the devices. Such a restriction is not as severe as it may first appear long term. Remember, in production the objective is to identify manufacturing defects, and such defects are going to be external to the devices.

# 10.20 MEMORIES AND MEMORY SYSTEMS

The strategy for debugging memories and memory systems follows directly from the techniques discussed in Chapter 4, Section 4.20, for testing memories and will not be repeated here.

# 10.21 APPLYING THE STRATEGY – SUBSYSTEM AND SYSTEM TEST

Once the individual modules are tested and their behavior has been confirmed, they are integrated and tested in larger subsystems until the complete system comes together. Many of the techniques used at the module level still apply.

Of critical concern as subsystems are built and tested are the more insidious dynamic and interaction problems that frequently occur as larger and larger portions of the system are integrated. Designing and building individual modules that perform a desired function is rather straightforward. Ensuring that several such modules function properly together when signal delays, noise, temperature, and other aberrations from the real world are at play is a more complex and challenging problem. Bringing all of the system modules together into a properly functioning product offers one the opportunity to use a myriad of engineering