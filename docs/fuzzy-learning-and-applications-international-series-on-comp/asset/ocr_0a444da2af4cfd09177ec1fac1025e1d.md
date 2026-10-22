where Δ₃′ = √(I²_{φ2c} + I²_{u2}) . For example, if one of the fuzzy rules is “IF u₂ is ILU₋₂ and e_{φ2c} is NE₋₃ THEN θ is z3 f₃(−2,−3)”, then this rule implies that the index I_{φ2c} = −3, I_{u2} = −2, and z3 f₃(−2,−3)=P B₃. By the Eq.(5.12) and (5.13), the intermediate output of the second stage is chosen as

u₂′ = GU₂(|∇u₂|) [ e_{φ1c} ; u₁ ] = GU₂( (|e_{φ1c}| e_{φ1c})/u₂ + (|u₁| u₁)/u₂ ) = GU₂ * f₂(e_{φ1c}, u₁) (5.31)

and the intermediate output of the first stage is chosen as

u₁′ = GU₁(|∇u₁|) [ e_{φ1t} ; e_x ] = GU₁( (|e_{φ1t}| e_{φ1t})/u₁ + (|e_x| e_x)/u₁ ) = GU₁ * f₁(e_{φ1t}, e_x) (5.32)

The rule-generated function for the intermediate outputs is obtained from f₂(e_{φ1c}, u₁) and f₁(e_{φ1t}, e_x) in which e_{φ1c}, u₁, e_{φ1t}, and e_x are replaced by their corresponding indices I_{φ1c}, I_{u1}, I_{φ1t}, and I_{e_x} of their fuzzy subsets, respectively,

f₂(I_{φ1c}, I_{u1}) = sat(n, - (|I_{φ1c}| I_{φ1c} + ρ₁ |I_{u1}| I_{u1}) / Δ₂′) (5.33) f₁(I_{φ1t}, I_x) = sat(n, - (|I_{φ1t}| I_{φ1t} + |I_x| I_x) / Δ₁′) (5.34)

where Δ₂′ = √(I²_{φ1c} + ρ₁ * I²_{u1}) and Δ₁′ = √(I²_{φ1t} + I²_x).

To take care of all the conditions, the fuzzy rule sets must be complete. The complete fuzzy rules can be determined by the rule-generated functions f₁, f₂, and f₃, and the corresponding three fuzzy rule bases are expressed in Figures 5.12, 5.13 and 5.14. The fuzzy set values of e_{φ1t}, e_{φ1c}, e_{φ2c}, e_x, u₁, u₂, and θ are shown in Fig. 5.11. These rule base sets are shown in Figures 5.12, 5.13 and 5.14, in which the fuzzy variables of the first stage are e_{φ1t}, e_x, and u₁, the fuzzy variables of the second stage are e_{φ1c}, u₁, and u₂, and the fuzzy variables of the last stage are e_{φ2c}, u₂, and θ. The output scaling factors are chosen as GU₃ = GU₂ = 1.