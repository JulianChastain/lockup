# lockup
## Intro
I was inspired by both [age](https://github.com/FiloSottile/age) and [encpipe](https://github.com/jedisct1/encpipe). I wanted to provide the secret key security of age with the simplicity of encpipe. The application can only encrypt (with -e flag) or decrypt (with -d flag). By default the application parses the argument after the flag as a file name, but passing '-' will read from standard input. It can do both encrypting and decryption sequentially (passing both flags). Passing no flags will cause the application to terminate immediately. 

## Internals
Files are encrypted with XSalsa20 and authenticated with a Poly1305 MAC (libsodium SecretBox). Keys are derived from argon2i with 16 bytes of random salt that are stored as the ciphertext header. I think this allows for low entropy passwords to be used securely. All primitives are provided by [PyNaCl bindings](https://pynacl.readthedocs.io/en/latest/).

## Example
![Example of both encrypting and decrypting a file](/pictures/example.png)
