# Minimize Variable Usage

Reducing the number of variables that each thread requires can help minimize the use of local memory. Prioritize using registers by optimizing the complexity of your kernels and reducing the scope and lifetime of variables where possible.