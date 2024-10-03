RSA is an example of what NIST calls IFC (integer factorization cryptography) - where the practical security comes via using what is sometimes called a “one-way function” — an operation that is computationally easy in one direction and hard in the other.

Integer factorization is a straightforward operation to understand for most people, and easy to implement correctly. It’s computationally very easy to multiply two large numbers and verify whether or not the result is what we expected. But going the other direction — given the result find the factors — grows substantially harder as the size increases. There are a few things to keep in mind:

Computational power grows quite rapidly, so what was computationally difficult at one point may be fairly easy 10 years later.
There is no proof that integer factorization is “hard” (see Integer factorization - Wikipedia for more info). We’ve made enormous gains in algorithms since RSA was first used, and it is much more efficient, but so far it still remains hard as long as the key size is ramped up.
In theory, quantum computating makes integer factorization a relatively efficient polynomial problem. Unlike symmetric cryptography (e.g. AES) where we can just double the key length to defeat QC, the amount of key length growth to prevent an efficient and large QC algorithm for integer factorization is impractical. The saving grace is that we’re nowhere near efficient and large QC algorithms (the record for Shor’s algorithm seems to still be factoring  
11
⋅
13
 , though some other methods have solved  
233
⋅
241
  and  
523
⋅
557
 ) .
Finding a polynomial time algorithm would lead to many people (generally theorists) classifying the problem as “easy.” But this doesn’t necessarily mean practically useful. The exponent and constants may be very large. This is akin to the AKS primality test, which indeed is a deterministic polynomial time algorithm, but it is never used in practice because the exponent is large enough that other deterministic tests such as ECPP and APR-CL are much faster for any practically-computable sized input. (Don’t confuse these with probabilistic tests such as Miller-Rabin or BPSW which are faster yet but not directly comparable). So maybe there is a “better” factorization algorithm found, but if it is only faster than existing methods for numbers with  
10
1000
  digits, then it has zero impact in practice.
Not specific to this, but do remember that there are a lot of moving parts to cryptography and rarely is the problem in the core operation. RSA breaks are usually in things like stupid bugs in the prime generation, or storing data in cleartext that probably shouldn’t have even been saved to begin with, or side-channel attacks, or good old human fallibility (“Hi, this is Joe from the Password Quality Department, we need to verify that your password is adequate. Read it slowly over the phone to me please.”)
All that mentioned, for your question, the keys for integer factorization cryptography (such as RSA) are (n,e) for the public key, and (n,d) for the private key. We see n is shared by both, and n is the product of two large primes ( 
n
=
p
⋅
q
 ). If we can factor n, then it is now a fairly trivial operation to get the private key (n,d) given the public key and the factorization. This blog article I found has a completely worked out example.
