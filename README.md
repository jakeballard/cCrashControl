CrashControl
============

A quick module for setting Windows Crash Dump settings. To be followed by a DSC Resource that configures the same.

Made possible and inspired by Bruce Mackenzie-Low's talk on Windows Debugging at Techmentor 2014. 

###(Get|Set)-CrashAlwaysKeep

When enabled this setting forces Windows 7 to keep the crash dump even if free space is low. By default Windows 7 will, under certain conditions, not create a MEMORY.dmp file.

For more info see: http://blogs.msdn.com/b/wer/archive/2009/02/09/kernel-dump-storage-and-clean-up-behavior-in-windows-7.aspx

###(Get|Set)-CrashOnCtrlScroll 

When enabled Windows will generate a crash dump when the 'Right‐Ctrl + Scroll Lock (twice)' keystroke is pressed.

Allows you to force a system memory dump from a keyboard. By default this function will enable the option for both USB and PS2 keyboards.

For more info see: http://msdn.microsoft.com/en-us/library/windows/hardware/ff545499(v=vs.85).aspx

###(Get|Set)-CrashDumpMode  

Sets the method of crash dump generation; 'None','Complete','Kernel','Small','Automatic'

For more info see: [Microsoft KB254649](http://support.microsoft.com/kb/254649)

###(Get|Set)-CrashNmiDump 

Enabling allows Windows to respond to a Non-Maskable Interrupt NMI signal from the hardware, which results in a Stop 0x80 bugcheck (NMI_HARDWARE_FAILURE)

   Windows Server 2012 & Windows 8 do not require NMICrashDump to be set.

For more info see: [Microsoft KB927069](http://support.microsoft.com/kb/927069)

   To generate an NMI on HP Hardware use the button on the system's iLO diagnostics page.

   To generate an NMI for a Hyper-V VM:
        debug‐vm “VM 1" ‐InjectNonMaskableInterrupt –Force

   To generate an NMI for a VMware VM see documentation here ([KB2005715](http://kb.vmware.com/selfservice/search.do?cmd=displayKC&docType=kc&docTypeID=DT_KB_1_1&externalId=2005715))

###Notes on crash dumps:
* Forcing a crash dump using keystroke or NMI is a good way to get a dmp file to analyze when the system is in a partially functional hang state.
* Some BIOS have an 'Automatic Server Recovery' setting which tries to detect if OS is live and resets. This will often interrupt the memory dump generation, and can be disabled to get a full dmp.
* A truncated dump file may still have usefull information. 
