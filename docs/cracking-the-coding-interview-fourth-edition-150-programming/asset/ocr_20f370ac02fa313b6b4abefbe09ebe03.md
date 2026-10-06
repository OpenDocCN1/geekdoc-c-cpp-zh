# Solutions to Chapter 12 | System Design and Memory Limits

```
while (in.hasNextInt()) {
    int n = in.nextInt();
    blocks[n / (bitfield.length * 8)]++;
}
```

```
for (int i = 0; i < blocks.length; i++) {
    if (blocks[i] < bitfield.length * 8){
        /* if value < 2/20, then at least 1 number is missing
        * that section. */
        starting = i * bitfield.length * 8;
        break;
    }
}
```

```
in = new Scanner(new FileReader("input_file_q11_4.txt"));
while (in.hasNextInt()) {
    int n = in.nextInt();
    /* if the number is inside the block that's missing numbers,
    * we record it */
    if (n >= starting && n < starting + bitfield.length * 8) {
        bitfield[(n-starting) / 8] |= 1 << ((n - starting) % 8);
    }
}
```

```
for (int i = 0; i < bitfield.length; i++) {
    for (int j = 0; j < 8; j++) {
        /* Retrieves the individual bits of each byte. When 0 bit
        * is found, the corresponding value. */
        if ((bitfield[i] & (1 << j)) == 0) {
            System.out.println(i * 8 + j + starting);
            return;
        }
    }
}
```