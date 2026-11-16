![](bbox=[0.15, 0.08, 0.92, 0.25])

Figure 1.1. Communication channel.

removed, the redundancy is then stripped off, and an estimate \(\widehat{\mathbf{x}}\) of the original message is produced. Hopefully \(\widehat{\mathbf{x}} = \mathbf{x}\). (There is a one-to-one correspondence between codewords and messages. Thus we will often take the point of view that the job of the decoder is to obtain an estimate \(\widehat{\mathbf{y}}\) of \(\mathbf{y}\) and hope that \(\widehat{\mathbf{y}} = \mathbf{c}\).) Shannon's Theorem guarantees that our hopes will be fulfilled for a certain percentage of the time. With the right encoding based on the characteristics of the channel, this percentage can be made as high as we desire, although not 100%.

The proof of Shannon's Theorem is probabilistic and nonconstructive. In other words, no specific codes were produced in the proof that give the desired accuracy for a given channel. Shannon's Theorem only guarantees their existence. The goal of research in coding theory is to produce codes that fulfill the conditions of Shannon's Theorem. In the pages that follow, we will present many codes that have been developed since the publication of Shannon's work. We will describe the properties of these codes and on occasion connect these codes to other branches of mathematics. Once the code is chosen for application, encoding is usually rather straightforward. On the other hand, decoding efficiently can be a much more difficult task; at various points in this book we will examine techniques for decoding the codes we construct.

# 1.1 Three fields

Among all types of codes, linear codes are studied the most. Because of their algebraic structure, they are easier to describe, encode, and decode than nonlinear codes. The code alphabet for linear codes is a finite field, although sometimes other algebraic structures (such as the integers modulo 4) can be used to define codes that are also called “linear.”

In this chapter we will study linear codes whose alphabet is a field \(\mathbb{F}_q\), also denoted GF(q), with q elements. In Chapter 3, we will give the structure and properties of finite fields. Although we will present our general results over arbitrary fields, we will often specialize to fields with two, three, or four elements.

A field is an algebraic structure consisting of a set together with two operations, usually called addition (denoted by +) and multiplication (denoted by · but often omitted), which satisfy certain axioms. Three of the fields that are very common in the study