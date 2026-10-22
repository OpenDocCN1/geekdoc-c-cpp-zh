# f₂( φ₁c , u₁ )

| eφ₁c \ u₁ | IRB-3 | IRU-2 | IRV-1 | IVE0 | ILV1 | ILU2 | ILB3 |
|---|---|---|---|---|---|---|---|
| NE-3 | IRB | IRB | IRB | IRB | IRB | IRV | IVE |
| NU-2 | IRB | IRB | IRU | IRU | IRV | IVE | ILV |
| NV-1 | IRB | IRU | IRV | IRV | IVE | ILV | ILB |
| ZR0 | IRB | IRU | IRV | IVE | ILV | ILU | ILB |
| PV1 | IRB | IRV | IVE | ILV | ILV | ILB | ILB |
| PU2 | IRV | IVE | ILV | ILU | ILU | ILB | ILB |
| PO3 | IVE | ILV | ILB | ILB | ILB | ILB | ILB |

Figure 5.13 Rule generated function f₂

φ'_{c,h} = φ'_{c,h} + θ
 u'_2 = u_2 + r cos(φ'_{c,h})
 v'_2 = v_2 + r sin(φ'_{c,h})
 φ'_{2t} = tan⁻¹( (v₁ - v'_2)/(u₁ - u'_2) )
 u'_1 = u'_2 + l cos(φ'_{2t})
 v'_1 = v'_2 + l sin(φ'_{2t})
 φ'_{1t} = tan⁻¹( (y - v'_1)/(x - u'_1) )