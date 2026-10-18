else return false; /\* No improvement in \(\mathcal{R}_i\) \*/

end.

Once node \(i\) computes its minimum region of residence, it tries to improve the minimum region of residence of each of its neighbors as follows:

Procedure improve_region

begin

for each \(j\in N(i)\) such that \(status_j\neq 1\) do

/\* Construct \(R_{ji}\), the viewed region of \(j\) \*/

\(R_{ji}=\mathcal{R}_i\oplus r_{ij};\)

Transmit \(R_{ji}\) to node \(j\);

endfor;

end.

The following location identification algorithm is executed by each node \(i\) until the node attains its stable region of residence \(\mathcal{S}_i\).

Algorithm location_region_identify

var region_change_flag : Boolean;

begin

while (true)

Get neighbor set \(N(i)\);

Generate \(RR_i\) : measure range with every neighbor \(j\in N(i)\);

region_change_flag = false;

repeat

Get T : viewed regions of residence \(R_{ij}\) from every neighbor \(j\);

if \(status_i=0\) then region_change_flag = compute_region(i, T);

improve_region(i, N(i), RR_i);

© 2016 by Taylor & Francis Group, LLC