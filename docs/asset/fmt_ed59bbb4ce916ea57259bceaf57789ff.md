
- **Implicit key authentication:** In this scheme, no unauthorized party should learn the session key `sk`, for find it, attacker computes first $P_S=Y_Sg$, $P_U=Y_Ug$, $uN_S=usg$, $sN_U=sug$, $MAC_S=H_2(ID_U^*||D_S||ID_S||P_S||P_U||uN_S)$ and time-stamp $T_3$. Hence, `usg` or `sug` is ECCDHP on ECC and $P_S=Y_Sg$, $P_U=Y_Ug$ which are similar to ECDLP in ECC.

- **Support anonymity property:** In MAKS, U computed $ID_{S1}=ID_S\oplus H_1(ID_S||ID_U)=ID_U\oplus H_1(ID_U||g)$ and sends to S. On getting $ID_{S1}$, S computes $ID_U^*=ID_{U1}\oplus H_1(ID_U||g)$ and uses this phase. Further, S computes $ID_{S1}=ID_S\oplus H_1(ID_S||g)$ and sends to U. On getting $ID_{S1}$, U computes $ID_S^*=ID_{S1}\oplus H_1(ID_S||g)$ and uses this phase. Hence, the presented protocol supports anonymity property.

### 15.5 Conclusion

This chapter has presented a secure and efficient identity-based mutual authentication protocol for cloud computing. This work has shown that it is secure and has many features and attributes such as key freshness, known session keys impersonation attack, PKG forward secrecy, replay attack, known session-specific attack, perfect forward secrecy, man-in-the-middle attack, mutual authentication, session key establishment, session key security, support anonymity property, and implicit key authentication. Further, this work proved that the framework is secured to launch safe communication channels via the unconfident channel. Future research also includes conserving the secrecy of the users’ information offered to the cloud server.

## References

Almorsy, M., Grundy, J., and Müller, I. (2016). An analysis of the cloud computing security problem. arXiv preprint arXiv:1609.01107.

Chang, H. and Choi, E. (2011). User authentication in cloud computing. In International Conference on Ubiquitous Computing and Multimedia Applications, pages 338–342. Springer.

Chen, T.-H., Yeh, H.-L., and Shih, W.-K. (2011). Advanced ecc dynamic id-based remote mutual authentication scheme for cloud computing. In 5th FTRA International Conference on Multimedia and Ubiquitous Engineering (MUE), 2011, pages 155–159. IEEE.

Dinesha, H. and Agrawal, V. K. (2012). Multi-level authentication technique for accessing cloud services. In International Conference on Computing, Communication and Applications (ICCCA), 2012, pages 1–4. IEEE.

Hankerson, D., Menezes, A. J., and Vanstone, S. (2005). Guide to elliptic curve cryptography. Computing Reviews, 46(1), 13.

Jing, X. and Jian-Jun, Z. (2010). A brief survey on the security model of cloud computing. In Ninth International Symposium on Distributed Computing and Applications to Business Engineering and Science (DCABES), 2010, pages 475–478. IEEE.

Khan, A. A., Kumar, V., and Ahmad, M. (2019). An elliptic curve cryptography based mutual authentication scheme for smart grid communications using biometric approach. *Journal of King Saud University-Computer and Information Sciences*, 2019. doi:10.1016/j.jksuci.2019.04.013.

Khan, N., Kumar, V., and Kumari, A. (2014). An identity-based secure authenticated framework by using ecc in cloud computing. *International Journal of Science and Research (IJSR)*, ISSN (online), pages 2319–7064.

Kumar, V., Ahmad, M., and Kumar, P. (2019a). An identity-based authentication framework for big data security. In Proceedings of 2nd International Conference on Communication, Computing and Networking, pages 63–71. Springer.

Kumar, V., Ahmad, M., and Kumari, A. (2019b). A secure elliptic curve cryptography based mutual authentication protocol for cloud-assisted tmis. *Telematics and Informatics*, doi:10.1016/j.tele.2018.09.001.

Kumar, V., Jangirala, S., and Ahmad, M. (2018). An efficient mutual authentication framework for healthcare system in cloud computing. *Journal of Medical Systems*, 42(8): 142.

Luo, M., Zhang, Y., Khan, M. K., and He, D. (2017). A secure and efficient identity-based mutual authentication scheme with smart card using elliptic curve cryptography. *International Journal of Communication Systems*, 30(16), 1–10.

Mishra, D., Kumar, V., and Mukhopadhyay, S. (2013). A pairing-free identity based authentication framework for cloud computing. In International Conference on Network and System Security, pages 721–727. Springer.

Nayak, S. K., Mohapatra, S., and Majhi, B. (2012). An improved mutual authentication framework for cloud computing. *International Journal of Computer Applications*, 52(5), 36–41.

Shamir, A. (1984). Identity-based cryptosystems and signature schemes. In Workshop on the Theory and Application of Cryptographic Techniques, pages 47–53. Springer.

Yang, J.-H. and Chang, C.-C. (2009). An id-based remote mutual authentication with key agreement scheme for mobile devices on elliptic curve cryptosystem. *Computers & Security*, 28(3–4): 138–143.

Zhang, Q., Cheng, L., and Boutaba, R. (2010). Cloud computing: state-of-the-art and research challenges. *Journal of Internet Services and Applications*, 1(1): 7–18.

Taylor & Francis

Taylor & Francis Group

`http://taylorandfrancis.com`

## 16 Development of a Statistical Yield Forecast Model for Rice Using Weather Variables Over Gorakhpur District of Eastern Uttar Pradesh

R. Bhatla, Rachita Tulshyan, Babita Dani, and A. Tripathi

## CONTENTS

- 16.1 Introduction................................................................................................................ 243
- 16.2 Materials and Method................................................................................................................ 245
- 16.3 Results and Discussion................................................................................................................ 246
- 16.3.1 Model Generated through SPSS................................................................................................................ 248
- 16.3.2 Validation................................................................................................................ 249
- 16.3.3 Crop Yield Forecast................................................................................................................ 250
- 16.4 Conclusions................................................................................................................ 254
- Acknowledgments................................................................................................................ 254
- References................................................................................................................ 254

### 16.1 Introduction

Rice is the staple food of the eastern and the southern parts of the country, particularly in the areas having over 1500 mm annual rainfall. Climate change has created one of the important challenges of the twenty-first century—to supply food for increasing populations, and to sustain the stressed environment, which also threatens global food security. The fourth assessment of the IPCC (Intergovernmental Panel on Climate Change) confirmed that in the last 100 years there has been an increase in atmospheric temperature of 0.74°C due to global warming and an expected increase in records of warmest year, frost, flood, heavy rainfall, etc. These changes have a tendency of posing likely threats to the ecosystem and to agricultural production all over the world. Agricultural productivity is most sensitive to climate change, as climate is the primary determinant of agricultural productivity [1].
