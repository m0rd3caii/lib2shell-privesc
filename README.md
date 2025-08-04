# lib2shell-privesc
Privilege escalation via SUID ssh-keygen abusing the -D flag to load a malicious shared object and spawn a shell with elevated privileges.


# lib2shell-privesc

This project demonstrates a simple privilege escalation technique by abusing a SUID `ssh-keygen` binary and the `-D` option, which loads a shared library as a PKCS#11 provider. By crafting a malicious shared object, we can spawn a shell with elevated privileges.

## Requirements

- A system where `ssh-keygen` is SUID (with effective UID 0 or a higher-privileged user).
- GCC or compatible C compiler.

## 🛠️ Compilation

Compile the shared object with:

```bash
gcc -fPIC -shared -o lib.so lib.c
```

Make sure the output file is named lib.so (or match whatever you want to load with -D).

## 🚀 Usage
Run the vulnerable ssh-keygen binary with:

```bash
./ssh-keygen -D ./lib.so
```
This will load the shared library, triggering the constructor function and spawning a root shell (if the effective UID of ssh-keygen is root).



