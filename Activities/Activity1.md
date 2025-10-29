**Try it (3–5 min): Detect Arm CPU features at runtime (no privileges)**

**Goal:** Turn the feature overview into a concrete capability map for
your machine by printing which Arm features are available at runtime.

**You’ll use:** a tiny C program that reads Linux’s auxiliary vector
(getauxval) and reports AArch64 HWCAP bits.

**Steps**

1.  Ensure build tools are present (Ubuntu/Debian):   
    `sudo apt update`  
    `sudo apt install -y build-essential`

2.  Using your favourite editor, create a file features.c with the
    following content:

> \#define GNU_SOURCE  
> *\#include \<stdio.h\>  
> \#include \<stdint.h\>  
> \#include \<sys/auxv.h\>  
> \#if defined(\_\_aarch64*\_\_)  
        > \#include \<asm/hwcap.h\> // HWCAP/HWCAP2 bit masks  
> \#endif // defined (\_\_aarch64\_\_)
>
> static const char\* yesno(int cond)  
> {  
> return cond ? "yes" : "no";  
> }
>
> int main(void)  
> {
>
> \#if !defined(\_\_aarch64\_\_)
>
  > printf("This program is intended for AArch64.\n");  
  > return 0;  
> \#else // !defined (\_\_aarch64\_\_)  
>
> // read hw capability registers  
> unsigned long hw1 = getauxval(AT_HWCAP);  
> unsigned long hw2 = getauxval(AT_HWCAP2);
>
  > // Vector & crypto features covered in the document
>
> printf("ASIMD/NEON: %s\n", yesno(hw1 & HWCAP_ASIMD));
> printf("AES: %s\n", yesno(hw1 & HWCAP_AES));
> printf("PMULL: %s\n", yesno(hw1 & HWCAP_PMULL));
> printf("SHA1: %s\n", yesno(hw1 & HWCAP_SHA1));
> printf("SHA2: %s\n", yesno(hw1 & HWCAP_SHA2));
> printf("CRC32: %s\n", yesno(hw1 & HWCAP_CRC32));
>
> \#ifdef HWCAP_SVE  
        > printf("SVE: %s\n", yesno(hw1 & HWCAP_SVE));  
> \#endif // HWCAP_SVE  
>  
> \#ifdef HWCAP2_SVE2  
        > printf("SVE2: %s\n", yesno(hw2 & HWCAP2_SVE2));  
> \#endif // HWCAP_SVE2  
        > return 0;  
> \#endif // !defined (\_\_aarch64\_\_)  
> }

3.  Build and run:   
    > gcc -O2 features.c -o features  
    > ./features

**You should see**

- Lines like `ASIMD/NEON: yes` (feature is supported).

- On **Neoverse-N1**: `SVE: no, SVE2: no` (SVE and SVE2 are not
  supported).

- On newer **V-series** with SVE/SVE2: these may be `yes`. (indicating
  support).

**Why it matters**

This gives you a real, local checklist of the vector/crypto features
discussed in the chapter. It also informs later build choices:  
- **Portable default:** `-march=armv8.2-a -mtune=\<neoverse-\*\>`   
- **Pinned to this CPU:** `-mcpu=\<your-neoverse\>`

