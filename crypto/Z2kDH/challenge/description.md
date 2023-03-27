# Introducing Z2kDH

Or, more precisely: $\mathbb{Z}/2^k\mathbb{Z}^*$-Diffie-Hellman

Sick of how slow it is to take the modulus of a large prime number?  
Tired of performing exponentiation over some weird group like ed25519?  
Just use the integers mod 2^k group!  
Efficient, reliable, doesn't require any hard math!

## Implementation details
**Group**: the cyclic group generated by $g=5$ in $\mathbb{Z}/2^{258}\mathbb{Z}$ ( $2^{256}$ elements)

Alice sends Bob $\lfloor (5^a \mod 2^{258}) / 4\rfloor$ (the last 2 bits are removed because they're always `01`)  
Bob sends Alice $\lfloor (5^b \mod 2^{258}) / 4\rfloor$ (dividing by 4 and flooring the result removes the 2 bits)  
Alice computes $\lfloor (5^b)^a \mod 2^{258} / 4\rfloor$  
Bob computes $\lfloor (5^a)^b \mod 2^{258} / 4\rfloor$  
Alice and Bob now share the secret key $\lfloor 5^{ab} \mod 2^{258} / 4\rfloor$

Offers 256-bit security<sup>[Citation Needed]</sup>  
Surely no one can break the discrete logarithm problem in polynomial time, right?

## Appendices
`alice_private_exponent.txt`: 256-bit hexadecimal number (removed due to security concerns)  
`bob_private_exponent.txt`: 256-bit hexadecimal number (removed due to security concerns)  
`output.txt`: public communication between Alice and Bob
- line 1: Alice sends her result to Bob, in hexadecimal format
- line 2: Bob sends her result to Alice, in hexadecimal format