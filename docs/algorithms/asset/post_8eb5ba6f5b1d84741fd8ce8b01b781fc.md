
## Chapter 1
Algorithms 31

# Alice

![](img/3dd1f1364df8f87b80683fc32a15b999_41_0.png)

# Bob

$e()$ is chosen that without knowing $d(-)$, Eve cannot do anything with the information she has picked up. In other words, knowing $e(x)$ tells her nothing about what $x$ might be.

For centuries, cryptography was based on what we now call *private protocols*. In such a scheme, Alice and Bob meet beforehand and choose a secret codebook, with which they encrypt all future correspondence between them. Eve's only hope, then, is to collect some encoded messages and use them to at least partially figure out the codebook.

Private-key schemes such as RSA are significantly more subtle and tricky: they allow Alice to send a message to Bob without ever having met before. Bob's encryption function $e()$ is publicly available, and Alice can encrypt her message with this function, *digitally locking it*. Only Bob has the key to quickly unlocking this digital lock: the decryption function $d(-)$. The point is that Alice and Bob need only perform calculations to lock and unlock message—operations that any computing device could handle. In contrast, to unlock the message without the key, Eve must perform operations like factoring large numbers, which requires more computational power than would be afforded by the world's most powerful computers combined. This compelling guarantee ensures web commerce, such as using credit card numbers over the Internet.

### 1.4.1 Private-key schemes: one-time pad and AES

If Alice wants to transmit an important private message to Bob, it would be of wise to scramble it with her encryption function,

> $e : (messages) \rightarrow (encoded messages).$

Of course, this function must be invertible—for decoding to be possible—and is therefore a bijection. Its inverse is the decryption function $d(-)$.

In the *one-time pad*, Alice and Bob meet beforehand and secretly choose a binary string $r$ of the same length—say, $n$ bits—as the important message $x$ that Alice will later send. Alice's encryption function is then a bitwise exclusive-or, $e(x)=x \oplus r$; each position in the encoded message is the exclusive-or of the corresponding positions in $x$ and $r$. For instance, if $r = 01110010$, the message $11110000$ is scrambled thus:

```
$e_r(11110000) = 11110000 \oplus 01110010 = 10000010$.
```

This function $e$ is a bijection from $n$-bit strings to $n$-bit strings, as evidenced by the fact that it is its own inverse!

```
$e(e(x)) = (x \oplus r) \oplus r = x \oplus (r \oplus r) = x \oplus \tilde{0} = x$.
```

where $\tilde{0}$ is the string of zeros. Thus Bob can decode Alice's transmission by applying the same encryption function a second time: $d(y) = y \oplus r$.

How Alice and Bob choose $r$ for this scheme? Simple: they should pick $r$ at random, flipping a coin for each bit, so that the resulting string is likely to be any element of $[0, 1]^n$. This will ensure that Eve intercepts the encoded message $y = e_r(x)$, she gets no information about $x$. Suppose, for example, Eve finds out $y=10$; what can she deduce? She doesn't know $r$, and the possible values it can take all correspond to original messages $x$:

![](img/3dd1f1364df8f87b80683fc32a15b999_42_0.png)

Given what Eve knows, all possibilities for $x$ are equally likely!

The downside of the one-time pad is that it has to be discarded after use, hence the second message encoded with the same pad would not be secure, because if Eve knew $x \oplus r$ and $z \oplus r$ for two messages $x$ and $z$, then she could take the exclusive-or to get $x \oplus z$, which might be important information—for example, (1) it reveals where zeros begin or end, and (2) if one message contains a long sequence of zeros (as could easily be the case if the message is another), then the corresponding part of the other message would be exposed. Therefore the random string that Alice and Bob share would be the length of all the messages they will need to exchange.

The one-time pad is a cryptographic scheme whose behavior and theoretical properties are completely clear. At the other end of the spectrum lies the advanced encryption standard (AES), a widely used cryptographic protocol that was approved by the U.S. National Institute of Standards and Technologies in 2001. AES is once again private-key: Alice and Bob have to agree on a shared string $r$. But the time string is of a fixed size, 128 to be precise (variants with 192 or 256 bits also exist), and specifies $e_r$ from 128-bit strings to 128-bit strings. The crucial difference is that this function can be used repeatedly, so for instance a long message can be encoded by splitting it into segments of 128 bits and applying $e_r$ to each segment.

The security of AES has not been rigorously established, but currently at present the general public does not know how to break the code—to recover $x$ from $c$—except using techniques that are not much better than the brute-force approach of trying all possibilities for the shared string $r$.

### 1.4.2 RSA

Unlike the previous protocols, the RSA scheme is an example of *public-key cryptography*: anybody can send a message to anybody using publicly available information, rather like addresses or phone numbers. Each person has a public key to the whole world and a secret key only to him or herself. When Alice wants to send message $x$ to Bob, she encodes $x$ using his public key. Bob decrypts it using his secret key, retrieve $x$. Eve is welcome to see all encrypted messages for Bob as she likes, but she will not be able to decode them, under certain simple assumptions.

The RSA scheme is based heavily upon number theory. Think of messages from Alice to Bob as modulo $N$; messages larger than $N$ can be broken into smaller pieces. The encryption function will then be a bijection. Its inverse is the decryption function $d(-)$.

**Property**
1. $x^e \equiv y \pmod N$ for $x \in \{0, \dots, N-1\}$.
2. $y^d \equiv x \pmod N$ for $y \in \{0, \dots, N-1\}$.

*Example.* Let $N=55$ and $e=3$. Since $\gcd(3, \phi(55)) = \gcd(3, 40) = 1$, there exists a unique $d$ such that $3d \equiv 1 \pmod{40}$. We find $d=27$. If Alice sends $x=13$, then $y = 13^3 \pmod{55} = 2197 \pmod{55} = 27$. To recover $x$, Bob computes $27^{27} \pmod{55} = 13$.

Proof. To show the mapping $x \mapsto x^e \pmod N$ is a bijection, we must show it is injective. If $x_1^e \equiv x_2^e \pmod N$, then $x_1 \equiv x_2 \pmod N$. This follows because $ed \equiv 1 \pmod{\phi(N)}$, so $(x_1^e)^d \equiv x_1^{ed} \equiv x_1^1 \pmod N$. Similarly for $x_2$. Thus $x_1 \equiv x_2 \pmod N$.
