# Looky-load

This looky, particularly focused on checking if malicious libraries are being loaded into processes or if the libc functions are being hooked. It does this by checking the LD_PRELOAD environment variable, the /etc/ld.so.preload file, and by verifying whether certain libc functions have been altered.
Features:

    Check LD_PRELOAD Environment Variable:
    The program checks if the LD_PRELOAD environment variable is set. This variable is commonly used by attackers to load malicious shared libraries into a process.

    Check /etc/ld.so.preload File:
    It checks if any shared libraries are listed in the /etc/ld.so.preload file, which can force the system to load specific libraries when a program starts.

![image](https://github.com/user-attachments/assets/1f5a7b29-5a1f-4170-9082-288b90dd1703)


    Check for Hooked Functions:
    The program checks if the common libc functions (like open, read, write, execve, etc.) are hooked. Hooking is when these functions are modified to behave in a different way, often used by malware to hide activities.


Compile:
``` gcc looky.c -o looky -ldl```
