to become more widely used in the future as more characters are encoded with values above FFFF hexadecimal. UTF-32 requires less sophisticated handling than UTF-16 in the presence of surrogate pairs. Figure L.1 shows the different ways in which the three encoding forms handle character encoding.

| Character | UTF-8 | UTF-16 | UTF-32 |
|---|---|---|---|
| LATIN CAPITAL LETTER A | 0x41 | 0x0041 | 0x00000041 |
| GREEK CAPITAL LETTER ALPHA | 0xCD 0x91 | 0x0391 | 0x00000391 |
| CJK UNIFIED IDEOGRAPH-4E95 | 0xE4 0xBA 0x95 | 0x4E95 | 0x00004E95 |
| OLD ITALIC LETTER A | 0xF0 0x80 0x83 0x80 | 0xDC00 0xDF00 | 0x00010300 |

Fig. L.1 | Correlation between the three encoding forms.

# L.3 Characters and Glyphs

The Unicode Standard consists of characters—written components (i.e., alphabets, numbers, punctuation marks, accent marks, etc.) that can be represented by numeric values. An example of such a character is U+0041 LATIN CAPITAL LETTER A. In the first character representation, U+yyyy is a code value, in which U+ refers to Unicode code values, as opposed to other hexadecimal values. The yyyy represents a four-digit hexadecimal number of an encoded character. Code values are bit combinations that represent encoded characters. Characters are represented using glyphs—various shapes, fonts and sizes for displaying characters. There are no code values for glyphs in the Unicode Standard. Examples of glyphs are shown in Fig. L.2.

The Unicode Standard encompasses the alphabets, ideographs, syllabaries, punctuation marks, diacritics, mathematical operators and other features that comprise the written languages and scripts of the world. A diacritic is a special mark added to a character to distinguish it from another letter or to indicate an accent (e.g., in Spanish, the tilde “~” above the character “n”). Currently, Unicode provides code values for 96,382 character representations, with more than 878,000 code values reserved for future expansion.

![](bbox=[0.115, 0.73, 0.85, 0.82])

Fig. L.2 | Various glyphs of the character A.

# L.4 Advantages/Disadvantages of Unicode

The Unicode Standard has several significant advantages that promote its use. One is the impact it has on the performance of the international economy. Unicode standardizes the characters for the world’s writing systems to a uniform model that promotes transferring and sharing data. Programs developed using such a schema maintain their accuracy be-