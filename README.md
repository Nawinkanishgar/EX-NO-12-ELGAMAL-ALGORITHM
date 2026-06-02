# EX-NO-12-ELGAMAL-ALGORITHM

## AIM:
To Implement ELGAMAL ALGORITHM

## ALGORITHM:

1. ElGamal Algorithm is a public-key cryptosystem based on the Diffie-Hellman key exchange and relies on the difficulty of solving the discrete logarithm problem.

2. Initialization:
   - Select a large prime \( p \) and a primitive root \( g \) modulo \( p \) (these are public values).
   - The receiver chooses a private key \( x \) (a random integer), and computes the corresponding public key \( y = g^x \mod p \).

3. Key Generation:
   - The public key is \( (p, g, y) \), and the private key is \( x \).

4. Encryption:
   - The sender picks a random integer \( k \), computes \( c_1 = g^k \mod p \), and \( c_2 = m \times y^k \mod p \), where \( m \) is the message.
   - The ciphertext is the pair \( (c_1, c_2) \).

5. Decryption:
   - The receiver computes \( s = c_1^x \mod p \), and then calculates the plaintext message \( m = c_2 \times s^{-1} \mod p \), where \( s^{-1} \) is the modular inverse of \( s \).

6. Security: The security of the ElGamal algorithm relies on the difficulty of solving the discrete logarithm problem in a large prime field, making it secure for encryption.

## Program:
```
#include <stdio.h> 
#include <stdlib.h> 
#include <me.h> 
#include <math.h> 
 
long long mod_pow(long long base, long long exp, long long mod) { 
    long long result = 1; 
    base = base % mod; 
    while (exp > 0) { 
        if (exp % 2 == 1) 
            result = (result * base) % mod; 
        exp = exp / 2; 
        base = (base * base) % mod; 
    } 
    return result; 
} 
 
long long mod_inverse(long long a, long long p) { 
    long long t = 0, newt = 1; 
    long long r = p, newr = a; 
    while (newr != 0) { 
        long long quo ent = r / newr; 
        long long temp = t; 
        t = newt; 
        newt = temp - quo ent * newt; 
        temp = r; 
        r = newr; 
        newr = temp - quo ent * newr; 
    } 
    if (r > 1) return -1; 
    if (t < 0) t += p; 
    return t; 
} 
 
int main() { 
    srand( me(0)); 
    long long p = 467; 
    long long g = 2; 
    long long x = rand() % (p - 2) + 1; 
    long long y = mod_pow(g, x, p); 
 
    long long m; 
    printf ("Enter the message (number < %lld): ", p); 
    scanf("%lld", &m); 
 
    long long k = rand() % (p - 2) + 1; 
    long long c1 = mod_pow(g, k, p); 
    long long c2 = (m * mod_pow(y, k, p)) % p; 
    long long s = mod_pow(c1, x, p); 
    long long s_inv = mod_inverse(s, p); 
    long long decrypted = (c2 * s_inv) % p; 
 
    printf ("Public values: p=%lld, g=%lld\n", p, g); 
    printf ("Private key: %lld\n", x); 
    printf ("Public key: %lld\n", y); 
    printf ("Original message: %lld\n", m); 
    printf ("Ciphertext: (%lld, %lld)\n", c1, c2); 
    printf ("Decrypted message: %lld\n", decrypted); 
 
    return 0; 
} 
```

## Output:
<img width="635" height="528" alt="image" src="https://github.com/user-attachments/assets/1d77de72-4679-4730-a22e-8dd85331ba9a" />


## Result:
The program is executed successfully.
