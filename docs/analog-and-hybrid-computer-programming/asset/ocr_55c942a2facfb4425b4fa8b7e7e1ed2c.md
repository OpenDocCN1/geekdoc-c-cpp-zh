```
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
```