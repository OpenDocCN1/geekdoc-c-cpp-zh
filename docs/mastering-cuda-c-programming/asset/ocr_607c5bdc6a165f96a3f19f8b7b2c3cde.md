# Minimizing Data Transfers

One fundamental strategy to reduce the performance impact of data transfers is to minimize the amount of data that needs to be transferred between the host and the device. This can involve several techniques:

Processing data directly on the device whenever possible to avoid sending it back to the host.

Using of overlap data transfers with computation whenever possible.

Structuring applications to maximize data reuse on the device, thus reducing the need for data transfers.