# kernel-module-smi-trigger

Linux kernel module for triggering a System Management Interrupt (SMI). See
[Wikipedia](https://en.wikipedia.org/wiki/System_Management_Mode) for generic
information about the System Management Mode (SMM) of x86 CPUs. See [SMI BIOS
Handler](http://blogs.phoenix.com/phoenix_technologies_bios/2008/12/bios-undercover-writing-a-software-smi-handler.html),
[BIOS & SMM Security Course](http://opensecuritytraining.info/IntroBIOS.html), and
[SMI & RTOS performance](https://de.slideshare.net/insydesoftware/bios-customizations-for-optimized-rtos-performance)
for more information about SMIs.

This kernel module creates a software SMI by writing a 0x0 to I/O port 0xb2 (the
SMI Command Port). After triggering such a SMI the CPU switches to SMM and
should return later to normal mode. This can take up to several hundreds of
microseconds - depending on the CPU. The module creates a char device in order
to interact with it (/dev/smitrigger).

For detecting happened SMIs on Linux, [smistat](https://github.com/ColinIanKing/debug-code/tree/master/smistat)
can be used that utilizes the msr kernel module.

## Usage

```bash
# Make kernel module
~ $ make

# Install kernel module
~ $ ./install-kernelmodule.sh

# Trigger a single software SMI
~ $ ./trigger.sh

# Remove kernel module
~ $ ./remove-kernelmodule.sh
```
