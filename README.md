Damgård–Jurik Cryptosystem
======
[Damgård–Jurik Cryptosystem](https://en.wikipedia.org/wiki/Damg%C3%A5rd%E2%80%93Jurik_cryptosystem) 
is a generalization of the [Paillier cryptosystem](https://en.wikipedia.org/wiki/Paillier_cryptosystem) ,
which is a additive [homomorphic cryptosystem](https://en.wikipedia.org/wiki/Homomorphic_encryption) . 
Please see [this paper](http://ojs.statsbiblioteket.dk/index.php/brics/article/viewFile/20212/17825)
for its mathematical proof.

For two message m1, m2, there exists

D(E(m1,r1)<sup>m2</sup>*g<sup>m2</sup>mod n<sup>2</sup>) = m1 * m2 mod n<sup>2</sup>

D(E(m1,r,)*E(m2,r2)mod n<sup>2</sup>) = (m1 + m2) mod n

For more details of Damgård–Jurik Cryptosystem, please see [this paper](https://people.csail.mit.edu/rivest/voting/papers/DamgardJurikNielsen-AGeneralizationOfPailliersPublicKeySystemWithApplicationsToElectronicVoting.pdf)

This library is for research on AHE or its applications,
there may be bugs that i overlook.

The GNU Multiple Precision Arithmetic Library (GMP) is used
for the underlying number theoretic operations, so you will need to
have that installed before building it.

####Install
You can build this library and include header file into your
project or you can copy the source and header file to your project.

To build this library

    cmake ./
    make
    make install

####Usage
Here we show a example to select a plaintext, please see header file for more info.

    #include <damgard_jurik.h>
    //Here we use libsodium as random number generator
    #include <sodium>

    damgard_jurik dj = damgard_jurik(50, 1024, randombytes_buf);
    damgard_jurik_plaintext_t text_1 = damgard_jurik_plaintext_t("abc");
    damgard_jurik_plaintext_t text_2 = damgard_jurik_plaintext_t("efg");

    damgard_jurik_plaintext_t sec_1 = damgard_jurik_plaintext_t((unsigned long)0);
    damgard_jurik_plaintext_t sec_2 = damgard_jurik_plaintext_t((unsigned long)1);

    damgard_jurik_ciphertext_t *c_1 = dj.encrypt(&sec_1, 10);
    damgard_jurik_ciphertext_t *c_2 = dj.encrypt(&sec_2, 10);

    damgard_jurik_ciphertext_t c_3 = (*c_1^*text_1_c) * (*c_2^*text_2_c);
    damgard_jurik_plaintext_t *se_p = dj.decrypt(&c_3);
    unsigned char *select_text = se_p->to_bytes();

