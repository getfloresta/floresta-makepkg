## Build floresta on arch linux

This repository contains a makepkg-based build for floresta, generating an antifact that can be installed with pacman.

The best way to use it is by first clonning the repository

```bash
$ git clone https://github.com/Davidson-Souza/floresta-makepkg
```

the check the pgp signature for the latest commit, this makes sure you're getting the code I wrote.

```bash
$ git verify-commit HEAD
```

this should result on something like:

```
gpg: Signature made Mon 27 Jan 2025 07:46:20 PM -03
gpg:                using RSA key ABBB04159EC09700AEF016D9F31869DC3DF97A86
gpg: Good signature from "Davidson Souza <me@dlsouza.lol>"
```

finally, build and install with

```
$ makepkg -si
```

After this, floresta should be running as a `systemd` service and available to connect with your wallet, or using the `floresta-cli` utility
