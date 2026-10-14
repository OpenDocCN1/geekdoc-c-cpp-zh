| User S | PKG |
|---|---|
| Sends < ID_S >
| ............→
| (via secure channel) | |
| | Generates x_S ∈ Z*_p |
| | Computes x_S = x_S g |
| | Computes h_S = H1(ID_S || X_S) |
| | Computes Y_S = x_S + M.h_S |
| | Sends < X_S, Y_S >
| | ← ............ |
| | (via secure channel) |
| Y_S g =? X_S + (H1(ID_S || X_S)) PK
| if verified then
| P_S = Y_S g |

FIGURE 15.3
Server private key extraction.

verifies T_S =? T_U . Further, S computes mutual authenticated code MAC_S = H2(ID*_U || ID_S || T_S || P_S || P_U || N_S), session key sk_S = H2(ID*_U || ID_S || P_U || P_S || MAC_S || N_S || T3), ID_S1 = ID_S ⊕ H1(ID_S || g) of S and sends message M2 = < N_S, ID_S1, T_S, s, MAC_S, T3 > via public channel.

# Step 3. On obtaining M2, U verifies T4 – T3 ≤ ΔT . Further, U computes ID*_S = ID_S1 ⊕ H1(ID_S || g) of S, mutual authenticated code MAC_S = H2(ID_U || ID*_S || T_U || P_S || P_U || N_U) and verifies MAC_U =? MAC_S. Thus, U authenticates to S and executes session key sk_S = H2(ID_U || ID*_S || P_U || P_S || MAC_U || N_U || T3).

Here, U and S ensure the validity of MAC_U = MAC_S. If successful, both U and S manage session key sk = sk_U = sk_S. Once the session key is established between U and S, they can communicate safely over a public communication channel. The details of this phase are shown in Figure 15.4.

# 15.4 Security Investigation

In this section, we have discussed security attributes and features which verify the presented protocol as:

+   - **Session key security:** In MAKS of this framework, U and S compute session following as:

+   - S computes session key sk_S = H2(ID*_U || ID_S || P_U || P_S || MAC_S || N_S || T3), and U executes session key sk_S = H2(ID_U || ID*_S || P_U || P_S || MAC_U || N_U || T3). E cannot executes the session key sk_S or sk_U where MAC_U = H2(ID_U || ID*_S || T_U || P_S || P_U || N_U) and MAC_S = H2(ID*_U || ID_S || T_S || P_S || P_U || N_S). MAC_S and MAC_U cannot be computed by E because of the definition hash function which is secured. Hence, the framework manages the session key.

+   - **Message authentication:** In MAKS, U and S verify message authentication property as: