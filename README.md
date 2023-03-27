# AES-256
---
This repository holds my implementation of AES-256 using ECB. It's the result of the project work I did whilst reading Cryptography (7.5 HP) at Högskolan Dalarna.
## Mode of Operation
---
This implementation uses [ECB, i.e. Electronic codebook](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Common_modes). The plaintext is broken down into 16 byte blocks, and is then, independent of any other blocks, encrypted into ciphertext. No block depends on any other block, and as a result, we are also able to decrypt each block individually. If an adversary performs cryptanalysis on it, it will, due to the lack of confusion, be easier to spot data patterns compared to when using CBC. ECB mode is <i>not</i> considered to be semantically secure, as just by examining the ciphertext from AES with ECB, we can potentially identify critical information about the plaintext.

## Confusion
[Confusion](https://en.wikipedia.org/wiki/Confusion_and_diffusion) of an element is essentially substitution of an element. With confusion, each bit of the ciphertext should depend on several parts of the key. The lack of confusion in e.g. Vigenere and substitution ciphers is one of the reasons that they're so so vulnerable to frequency analysis.
<br>
<br>
In AES, we mainly handle confusion through $subBytes()$, a method that substitutes each element of the block with its corresponding element in the S-box, i.e. substitution-box.

## Diffusion
---
Changing a character of plaintext will significantly change the ciphertext when using a cipher that holds the property [diffusion](https://en.wikipedia.org/wiki/Confusion_and_diffusion).
<br>
<br>
In AES, we mainly handle diffusion through $shiftRows()$ and $mixColumns()$. We use $shiftRows()$ to shift each row to the left the same number of steps as the current row number, and $mixColumns()$ to shuffle each column in the block using lookup-tables.

## Performance
---
There are certainly things I can do to improve the performance of my code. I could reduce the amount of nested for loops ($O(n^2)$ time complexity), reduce the amount of conversions between different data types, such as lists, strings, and integers. All my methods are dependent on the blocks being in 2D list format, so here and there I need to flatten the lists, and vice versa, transform it from 1D to 2D again. Using 2D lists have however added the benefit of being able to easier understand the code, and they have in general just been easier to work with, in my opinion. I believe working with blocks as 1D lists or even strings (immutable) can be quite frustrating and nonintuitive sometimes, so that's why I decided to use 2D lists instead, even though it might cost me processing speed. Either way, the main goal of this project was to implement AES, so performance wasn't really optimized and prioritized so it could definitely be improved.
