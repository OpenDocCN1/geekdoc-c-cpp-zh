
![](img/91599d88757ed8c75960eb83f4f85a12_215_0.png)

### Fig. 7.3. Computer program for solving the one-dimensional wave equation

The corresponding configuration file for the hybrid controller looks basically like the minimal example shown on page 197 with the following changes and additions:

```yaml
wave_equation.yml
elements:
  U1: O260
  U2: O261
  U3: O262
  U4: O263
problem:
  times:
    ic: 10
    op: 200
  ro-group:
    - U1
    - U2
    - U3
    - U4
```

The problem-section has been added. It contains the various timing settings, the definition of a readout group (ro-group) and other optional subsections which are not required here. The readout group defines a list of computing elements which will be read during the OP phase of the simulation at equally-spaced intervals. In this case the readout group consists of the elements labelled U1, U2, U3, and U4.

The corresponding Perl program using this configuration file is shown below:

```perl
use strict;
use warnings;
use IO::HyCon;

my $ac = IO::HyCon->new();  # Create a new hybrid controller object.
$ac->setup();               # Setup the analog computer
$ac->single_run_sync();     # Start a single run.
$ac->get_data();            # Get the data gathered
$ac->plot();                # and generate a plot.
```

The method call $ac->setup() performs all basic setup operations such as setting initial and operating times as well as defining the readout group if one is specified in the configuration file. If such a group is defined, data will be gathered automatically by the hybrid controller during each analog computer run. The data gathered is stored in the $ac object and can be extracted by calling the method $ac->get_data() which returns an array reference. Another useful method is $ac->plot() which can be parameterized to yield different plotting styles and requires that gnuplot is installed on the digital computer.

Just calling $ac->plot() as in the example above yields the result shown in figure 7.4. The four lines in the graph represent the four variables u1,...,u4. Each variable represents one location along the x-axis of the one-dimensional wave equation problem.

In problems like this it would be nicer to have a more 3d-ish display of the variables being recorded. The plot() method supports such a display style, too. Calling $ac->plot(type => '3d') yields the plot shown in figure 7.5 which is much more intuitive than the overlaid 2d plots shown previously.

![](img/91599d88757ed8c75960eb83f4f85a12_219_0.png)

### Fig. 7.6. Modified setup for the inverted pendulum

![](img/91599d88757ed8c75960eb83f4f85a12_220_0.png)

### Fig. 7.7. Control circuit for the controlled inverted pendulum

```python
import serial

from readchar import readchar
from time import sleep

# Hybrid Controller serial setup
HC_PORT = "/dev/cu.usbserial-DN050L10"
HC_BAUD = 250000
HC_BYTE = 8
HC_PARITY = serial.PARITY_NONE
HC_STOP = serial.STOPBITS_ONE
HC_RTSCTS = False
HC_TIMEOUT = 2

# Addresses of the computing elements to be read
HC_SIM_X_POS = "0223" # Position of the cart
HC_SIM_X_VEL = "0222" # Velocity of the cart
HC_SIM_ANGLE = "0161" # Angle of the pendulum
HC_SIM_ANGULAR_VEL = "0160" # Angular velocity of pendulum

HC_SIM_DIRECTION_1 = "D0" # Digital out 0=1: push right
HC_SIM_DIRECTION_0 = "d0" # Digital out 0=0: push left
HC_SIM_IMPULSE_1 = "D1" # Digital out 1=1: apply force
HC_SIM_IMPULSE_0 = "d1" # Digital out 1=0: stop applying force

# Model-1 Hybrid Controller: commands and responses
HC_CMD_RESET = "z" # Reset hybrid controller
HC_CMD_INIT = "i" # Initial condition
HC_CMD_OP = "o" # Start simulation run
HC_CMD_ROGROUP = "f" # Define a readout group

HC_RSP_RESET      = "RESET" # HC response to HC_CMD_RESET

# Send a command to the hybrid controller
def hc_send(cmd):
    global dbg_last_sent
    dbg_last_sent = cmd
    hc_ser.write(cmd.encode("ASCII"))

# Get a response from the hybrid controller
def hc_receive():
    # As the hybrid controller ends each output with
    # "\n", we can conveniently use readline
    return hc_ser.readline().decode("ASCII").split("\n")[0]

# When reading values from the hybrid controller, the result
# is formatted as "<value><space><id/type>\n". The type
# information is ignored in the following.
def hc_res2float(str):
    f = 0
    try:
        f = float(str.split(" ")[0])
        return f
    except:
        print("ERROR #2: FLOAT CONVERSION:", str)
        print("Last command sent:", dbg_last_sent)
        print("Length of received string:", len(str))
        print("Hex output of received string:","".join("{:02x}".format(ord(c)) for c in str))
        sys.exit(2)

# Query the current state of the simulation, which consists of
# the position and the velocity of the cart, and the angle and
# angular velocity of the pendulum
def hc_get_sim_state():
    hc_send(HC_CMD_ROGROUP)
    (res_x_pos, res_x_vel, res_angle, res_angle_vel) =
        hc_receive().split(',')
    return (hc_res2float(res_x_pos), hc_res2float(res_x_vel),
            hc_res2float(res_angle), hc_res2float(res_angle_vel))

# Reset the simulation (pendulum is in its upright position,
# cart is at x = 0)
def hc_reset_sim():
    hc_send(HC_CMD_INIT)
    sleep(0.05)        #time for condensators to recharge
    hc_send(HC_CMD_OP)
    sleep(0.05)        #time for the feedback string to arrive
    hc_ser.flushInput()

# Push the cart to the left or right, depending on the parameter a
def hc_influence_sim(a):
    if (a == 1):
        hc_send(HC_SIM_DIRECTION_1)
    else:
        hc_send(HC_SIM_DIRECTION_0)

    hc_send(HC_SIM_IMPULSE_1)
    sleep(HC_IMPULSE_DURATION / 1000.0)
    hc_send(HC_SIM_IMPULSE_0)

# Initialize the serial line
try:
    hc_ser = serial.Serial(port=HC_PORT,
                           baudrate=HC_BAUD,
                           bytesize=HC_BYTE,
                           parity=HC_PARITY,
                           stopbits=HC_STOP,
                           rtscts=HC_RTSCTS,
                           dsrdtr=False,
                           timeout=HC_TIMEOUT)

    sleep(1.5)
    dbg_last_sent = ""
except:
    print("ERROR #1: SERIAL PORT CANNOT BE OPENED.")
    sys.exit(1)

# Reset the hybrid controller
received = ""
while (received != HC_RSP_RESET):
    print("Hybrid Controller reset attempt...")
    hc_send(HC_CMD_RESET)
    sleep(1)
    received = hc_receive()
    if received != "":
        print("  received:", received)

# Define the readout group for all four parameters
hc_send('G' + HC_SIM_X_POS + ',' + HC_SIM_X_VEL + ',' + HC_SIM_ANGLE + ',' + HC_SIM_ANGLE_VEL + '.')
# Here follows the actual reinforcement learning code...
...
r1.py
```

Using the analog computer as its sparring partner the reinforcement learning systems learns to balance the inverted pendulum based on the values x, ẋ, φ, and φ̇. Whenever φ exceeds about 30 degrees or the cart position x leaves the interval [−1,1] the current simulation run is terminated and the next run is started. At first, the reinforcement learning system balances rather randomly but improves quickly over time. At the end of the training the pendulum is held in a stable position more or less indefinitely.¹⁴⁶

## CHAPTER 8 Summary and outlook

Programming analog, and therefore hybrid computers, is fundamentally different from the algorithmic approach used in digital computers as the preceding chapters have shown. At first sight, using an analog computer seems to be much more involved and complicated than programming a digital computer. This is deceptive. Apart from the scaling issues, programming analog computers is much more straightforward than programming digital computers because the mathematical description of a problem is basically enough to set up an analog computer – while in the case of a digital computer a plethora of additional quirks and complications have to be taken into account.

The main advantages of analog computers, either as stand-alone systems or as part of a hybrid computer setup, are

- the extremely high degree of parallelism that this class of machines exhibits,
- the equally high energy efficiency, and
- the stability of solutions obtained by analog computers – for example, there is nothing like numerical instability.

Every change of a bit from 0 to 1 or vice versa in a digital computer requires a small parasitic capacitance to be charged or discharged. Together with other effects, such as the structure of typical output driver stages of logic gates, this results in a superlinear relationship between clock frequency and the overall energy consumption of a digital computer. Given today’s clock frequencies of up to several GHz this results in power requirements of way over 100 W for a typical multi-core
