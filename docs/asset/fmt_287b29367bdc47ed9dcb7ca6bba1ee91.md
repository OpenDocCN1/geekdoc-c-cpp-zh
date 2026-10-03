
# RSA 和 Diffie-Hellman 是最流行的公钥方法

RSA 和 Diffie-Hellman 是最流行的公钥方法，它们是现代密钥管理协议（如 `IKE` [RFC2409] 和 `TLS` [RFC2246]）的基础。这些协议通过迭代交换公密钥和其他密钥管理信息，因此更不易泄露，并通过定期更换密钥来限制受保护的数据量。为了使公钥发挥作用，节点必须信任节点身份与其公钥之间的关联。由作为传感器网络认证机构的受信机构会为每个传感器设备生成一个唯一的证书。传感器设备通常通过在线交换获取公钥证书。Eschenauer、Perrig 和 Bauer 使用了不同的方法来生成、分发和发现信任。Stajano 和 Anderson 使用了一种激进的方法，这种方法对于节点大部分时间处于节能睡眠状态的传感器网络可能是实用的。

## 密钥建立

一旦建立了信任，就会使用密钥协商或密钥传输协议来建立密钥。密钥协商允许两个节点贡献用于创建密钥的密钥管理信息。双方贡献可以防止一方故意或无意地导致弱密钥的使用。密钥传输发生在一个节点生成秘密密钥并将其发送给另一个节点时。`RSA` 最经常通过接收者的公钥加密秘密密钥来保护密钥传输。基于 `Diffie-Hellman` 的 `ElGamal` [ElGamal] 也可用于此目的。尽管密钥传输不像密钥协商那样具有贡献性，但它可以减少必须交换的交互式密钥管理消息的数量。

## 计算与通信开销

`RSA` 和 `Diffie-Hellman` 需要大量的计算，使得它们对大多数传感器网络来说没有吸引力。这两种协议都执行模运算，这在大多数传感器设备计算受限的微处理器上需要数百万次指令。结果是执行 `RSA` 和 `Diffie-Hellman` 操作需要几秒钟（或更长时间），这显著增加了建立密钥的延迟。由于大多数传感器在不使用时会返回耗能的睡眠状态，额外的计算时间会消耗更多能量。比计算更严重的问题是 `RSA` 和 `Diffie-Hellman` 协议所需的通信所消耗的能量和产生的延迟。公证书和其他公钥管理信息需要交换数千个位。这些通信消耗了发送者和接收者的发射能量。此外，节点之间发送信息所需的时间引入了巨大的延迟。这种延迟实际上远大于位数乘以数据速率的数值，因为计算和通信对能量消耗和延迟的影响之和通常使得这些协议不适用于传感器网络。

## 椭圆曲线密码学 (ECC)

`ECC` [Menezes] 是传感器密钥管理中相比 `RSA` 和 `Diffie-Hellman` 极具吸引力的替代方案。基于椭圆曲线的 `Diffie-Hellman` 密钥生成在相同安全水平下需要少的计算和通信。例如，160 位的 `ECC` 在安全性上约等于 1024 位的 `RSA` 密钥 [Johnson]。`ECC` 系统的最小证书约为 62 字节，而 `RSA` 系统为 256 位 [Johnson]。随着这些技术的成熟并获得更广泛的接受，基于 `ECC` 的方案已添加到 `IKE` 等其他标准中。

### 8.6.4.3 基于身份的加密

`Shamir` 在传感器网络中特别有吸引力，因为它显著减少了密钥消息。受信机构根据每个传感节点的身份生成私钥。传感器节点从传感器设备身份中派生公钥，在执行密钥管理协议时消除了公密钥的交换。Maurer 和 Jacobi 描述了一种方案 [Maur]，消除了交换身份之外任何内容的需求。尽管他们的方案在密钥密钥需要离线计算，但 Matt 对最近开发的基于身份的椭圆曲线方案提供了概述，这些方案并没有这个问题。

### 8.6.4.4 组密钥管理

当需要加密或消息认证来保护广播或多播通信时，就需要组管理协议。目前很少有组管理协议被标准化，更不用针对传感器网络环境了。组协商协议如 `Group Diffie-Hellman` [Steiner] 和 `Burmester-Desmed` [Burmester] 即使使用 `ECC` 密钥也大量的通信。Matt 发明了一种结合了基于身份的加密和组密钥传输的组密钥方案，并用于陆军传感器网络 [Carman]。

## 数据安全视角

## 8.7 其他来源

## 8.8 总结

如何为传感器网络提供最佳的数据安全，很大程度上取决于目标环境的独特需求和限制。然而，我们已经识别出标准机制，可以针对各种数据安全威胁提供有效的数据保护。加密和消息认证最好在链路层和网络层提供，具体取决于是否进行了传感器数据融合。当进行传感器数据融合时，应该实现跳跳认证和消息认证。当不需要融合时，跳跳认证和端到端加密是一种有效的多层保护。

在选择安全算法时，需要一个强有力的理由来不使用 `AES` 进行加密。当使用至少 128 位的密钥时，`HMAC-SHA-1`、`HMAC-MDS` 或基于 `AES` 的 `OMAC` 可以对常规传感器数据消息提供强认证。在密钥管理、路由和传感器数据操作等重要操作期间，应使用 `ECDSA` 对数据进行签名。

由于传感器网络环境中带宽有限且节点无人值，密钥管理和路由协议的安全面临巨大挑战。强密钥管理需要偶尔交换密钥管理消息和公共计算，这会消耗资源受限设备的能量并增加延迟。`ECC` 在与公共基础设施结合或使用基于身份的方案时，为流行的 `RSA` 和 `Diff-Hellman` 算法提供了一种高效的替代。需要保护链路层广播或网络层组播的组密钥管理更具挑战性。传统的 `hoc` 路由需要细分，并针对特定协议提供保护以成功提供传感器数据的可用性。

# 参考文献

- [Asada] Asada, G. et al., Wireless integrated sensor networks: Low power systems on a chip, European Solid State Circuits Conference, The Hague, the Netherlands, October 1998.
- [Biham] Biham, E. and Shamir, A., Differential Cryptanalysis of the Data Encryption Standard, Springer-Verlag. Berlin, Germany, 1993.
- [Burmester] Burmester, M., and Desmedt, Y., A secure and efficient key distribution system, Proceedings of Security '94, Lecture Notes in Computer Science 950, pp. 275–286, 1995.
- [Carman] Carman, D. and Circione, G., Energy and latency of communicating certificates during secure network initialization of sensor networks, Proceedings of Collaborative Alliance Conference 2003, College Park, MD, 2003.
- [Carman2] Carman, D. and Boncelet, C., A new message authentication approach with less overhead and greater reliability, Proceedings of Collaborative Technology Alliance (CTA) Communications & Networks (C&N) Alliance 2003 Annual Symposium, College Park, MD, April 2003.
- [Carman3] Carman, D., Cincione, G., and Matt, B., Energy-efficient and low-latency key management for sensor networks, Proceedings of the 23rd Army Science Conference, Orlando, FL, December 2–5, 2002.
- [Denning] Denning, D., Information Warfare and Security, Addison-Wesley, Reading, MA, 1999.
- [Dobbertin] Dobbertin, H., Cryptanalysis of MD5 complex, German Information Security Agency, May.
- [Dworkin] Dworkin, M., NIST Special Publication 800-38A—Recommendation for block cipher modes of operation—Methods and techniques, National Institute of Standards and Technology (NIST), Gaithersburg, MD, December 2001.
- [ElGam] ElGam, T. A public cryptosystem and a signature scheme based on the discrete logarithm, IEEE Transactions on Information Theory, 31(4):469–472, 1985.
- [Eschenauer1] Eschenauer, L. and Ligor, V., A key-management scheme for distributed sensor networks, Proceedings of the Ninth ACM Conference on Computer and Communications Security 2002, Washington, DC, 2002.
- [Eschenauer2] Eschenauer, L., Ligor, V., and Bars, J. On trust establishment in mobile ad-hoc networks, Proceedings of the Security Protocols Workshop, Cambridge, U.K., April 2002.
- [FIPS46-3] U.S. Department of Commerce, National Institute of Standards and Technology (NIST), Encryption Standard (Federal Information Processing Standards Publication 46-3), October 1999.
- [FIPS186-2] U.S. Department of Commerce, National Institute of Standards and Technology (NIST), Digital Signature Standard (DSS) Federal Information Processing Standards Publication 186-2, January 2000.
- [FIPS197] U.S. Department of Commerce, National Institute of Standards and Technology (NIST), Advanced Encryption Standard (AES) (Federal Information Processing Standards Publication 197), November 26, 2001.
- [FIPS180-2] U.S. Department of Commerce, National Institute of Standards and Technology (NIST), Secure Hash Standard (Federal Information Processing Standards Publication 180-2), August 2002.
- [Lligor] Ligor, V. and Donescu, P. Fast encryption and authentication: XCBC encryption and XCB authentication methods, Presented at the Second NIST Workshop on AES Modes of Operation, Santa Barbara, CA, August 24, 2001.
- [ISO7498] International Organization for Standardization (ISO), Information processing systems reference model, ISO 7498, 1984.
- [Johnson] Johnson, D., ECC, Fault resiliency,, 2002.
- [Julia] Julia, C., Energy-efficient and low-latency key management for sensor networks, Proceedings of the 23rd Army Science Conference, Orlando, FL, December 2–5, 2002.
- [Law] Law, Y., Denial of service in sensor networks, IEEE Computer, 35(10):54–62, 2002.
- [Matt] Matt, B., Potential vulnerabilities in wireless protocols, Proceedings of the 23rd Army Science Conference, Orlando, FL, December 2–5, 2002.
- [Matsui] Matsui, M., Linear cryptanalysis, IEEE Transactions on Information Theory, 31(4):469–472, 1985.
- [Maurer] Maurer, U., Random key, 1993.
- [Wiener] Wiener, R., The MD5-digest algorithm, RFC 1321, April 1992.
- [Rogaway] Rogaway, P., et al., OCR: A block-cipher mode of operation for authenticated encryption, ACM Conference on Computer and Communications Security (CCS-8), Philadelphia, PA, ACM Press, New York, pp. 196–205, 2001.
- [Schneier] Schneier, B., Applied Cryptography, 2nd ed., John Wiley & Sons, New York, 1996.
- [Shamir] Shamir, A., Identity-based cryptosystems and signature schemes, Proceedings of Crypto'84, New York, pp. 47–53, 1985.
- [Stallings] W., Cryptography and Network Security: Principles and Practice, 3rd ed., Prentice Hall, Upper Saddle River, NJ, 2003.
- [Stajno] Stajano F. and Anderson, R., The resurrecting: Security issues for ad-hoc wireless networks, Security Protocols, Seventh International Workshop, 1999.
- [Steiner] Steiner, M., Tidik, G., and Wainer, M., Key agreement in dynamic peer groups, IEEE Transactions on Parallel and Distributed Systems, 118(8):769–780, 2000.
- [Wilkinson] Wilkinson, R. U. says GPS sites destroyed, Iraq Crisis Bulletin/(INEWS) International News E-Wire Service, Doha, Qatar, March 26, 2003.
- [Wood] Wood, A. and Stankovic, J., Denial of service in sensor networks, IEEE Computer, 35(10):54–62, 2002.
- [WTLS] Wireless Application Protocol Forum, Ltd., WAP transport layer end-to-end security, 2001.
- [Zhu] Zhu, F., Security for ad hoc networks (including sensor networks) web, http://www.ccs.edu/home/zhufeng/security_manet.html.

![](img/11e8580124e6543d23c6c1d715727b6a_977_0.png)

# 基于随机密钥预分布的传感器网络安全

**Lianyu Zhao**  
克利姆森大学

**Richard R. Brooks**  
克利姆森大学

**Brijesh Pillai**  
克利姆森大学

**P.Y. Govindarajaju**  
克利姆森大学

**Matthew Pirretti**  
宾州立大学

**Vijayakrishnan Narayanan**  
宾州立大学

**Mahmut Kanderim**  
宾州立大学

+ 9.1 引言 ................................................................201
