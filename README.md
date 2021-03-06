Signify ported from OpenBSD to Linux
=====================================
[![build status](https://hub.blitznote.com/src/signify/badges/master/build.svg)](https://hub.blitznote.com/src/signify/commits/master)

with these differences:
 * Randomness is provided by syscall 'getrandom' (Linux ≥3.18)
 * or RDRAND.
 * Compiles to a static binary of less than 180KiB (less than 270KiB with *Seccomp* and *musl-libc*).

The resulting binary is licensed under the same terms as OpenBSD's *signify*.
For the sources — please see the source files for their licensing terms,
and if you are permitted to use them in another work.

Usage
------

In this example the binary file *signify* gets signed and verified:
```bash
# generate a keypair
$ signify -G -c "W. Mark Kubacki <wmark@hurrikane.de>" -p mark.pub -s mark.sec

# sign (usually a small file, like the output of: sha512sum …)
$ signify -S -x signify.sig -s mark.sec -m signify

# verify
$ signify -V -x signify.sig -p mark.pub -m signify
Signature Verified
```

Let X be the message (»file«), if X{,.sig} exist the signature file gets found automatically and you can write:
```bash
$ signify -V -p mark.pub -m X
Signature Verified
```
