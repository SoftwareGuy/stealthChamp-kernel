# StealthChamp Kernel: Vanilla Linux kernel with stealth KVM modules

## What is this?

This is a fork of the Linux kernel 5.9.10 release source code with stealth KVM patches. Nothing else was modified, it's basically a vanilla kernel with some KVM patches. Basically, I did the hard part of patching the kernel for you. Just build and install the bloody thing.

I have successfully compiled and used this kernel to inspect some suspicious software that was avoiding my Windows 10 workstation virtual machine. It also has been reported to bypass Virtual Machine checks in conjuction with other patched software on Genshin Impact, some VM-detecting application packers/anti-tamper and anti-cheat.

## Compiling

- Compile as you would with a normal kernel. Make sure you have all the dependenices installed. `make menuconfig`, `make bzImage`, `make modules`, `sudo make install && sudo modules_install`.
- Include `-j<CPUs>` after the make, like `make -j5` if you have a six-core processor. Personally, I use CPU core count - 1, which allows one core to be used for your host while compiling.
- Unless you know what you're doing, when in `make menuconfig`, load the sample config included in this repository as it will give you a kernel config provided by Ubuntu's kernel. This is more than enough.
- One thing to note is that the patch does normally cause the compile to fail due to ISO C99 restrictions, how you can't have a variable being initialized by the return of another function or something silly. I had to modify the Makefile to bypass this warning, since it was being treated like an error.

## Stability Warning

I have noticed one or two full kernel lockups while running this kernel, however I do not think they are related specifically to the KVM patch. It may have been glitches on the testing hardware.

Please don't use as a daily driver kernel unless you know what you're doing. **Neither myself or the original patch author take any responsibility for any data lost or damaged by use of this kernel!!** 

## For use with Intel-based VM hosts only.
For AMD-based virtualization machines, you'll need to patch the kernel with BetterTiming, which is available at https://github.com/SamuelTulach/BetterTiming . This kernel is only patched for Intel-based VM hosts (Intel VMX).

Running this kernel without BetterTiming on AMD will not give you any timing patches.

## Sources

- This kernel fork wouldn't be here today with out the RDTSCv2 patch provided over at https://gitlab.com/DonnerPartyOf1/kvm-hidden.
- The Linux Kernel 5.9.10 source was pulled from the Linux Kernel archives at http://kernel.org.

## What else do I need?

- See my other repositories for a stealth version of QEMU which snuggles up nicely to this kernel.

## Credits

I take no credit for what CB/DonnerPartyOf1 did, I am merely providing a repository with the patch applied to help people who need to reverse engineer suspicious applications inside Virtual Machines (KVM/QEMU) or run a kernel that can fool anti-VM software.

Enjoy.
