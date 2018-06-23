**Note: I recently updated my PC to 10.13.2, I put my EFI/CLOVER directory for macOS 10.13.2 in `10.13.2` directory. Have fun!**

**As @[Tomygames](https://github.com/Tomygames) suggested at [here](https://github.com/NTT123/Hackintosh-HP-Z420-MacOS-High-Sierra-10.13/issues/5#issuecomment-368083010). You need to "[a]ctivate Legacy ACPI CPU Tables in BIOS".**

**Some detailed instructions to install macOS provided by @spellbound can be found [here](https://github.com/NTT123/Hackintosh-HP-Z420-MacOS-High-Sierra-10.13/issues/5#issuecomment-399620392).** 

How to install MacOS Sierra 10.12.3 on HP Z420 Workstation.

Overall, we will use Unibeast to create a USB Installer.

From my Mac OS X 10.10 or 10.11, download macOS Sierra Installer (go to App Store to download).

Then, we use the recent Unibeast (UniBeast 7.0.1) to create a bootable USB. However, we **have to** use kexts from **CustoMac Essential** package and put these kexts to /Volumes/EFI/EFI/CLOVER/kexts/Other/ directory (mount your EFI partition first!)

### Here the Tricks 

Note: I put my `/Volumes/EFI/EFI/CLOVER` directory and all kexts we need in the repo.

- Install the lastest CLOVER (e.g., v2k4)

- We have to use flag `npci=0x2000` all the time.  (I also use `dart=1`)

- Z420 crashes randomly when booting, we can fix that with flag `cpus=1`. However, this makes our PC slow (only 1 CPU!!), therefore, we fix this problem by installing `VoodooTSCSync.kext` at `/System/Library/Extensions` .  Remember to fix permission.  E.g.    

     chmod -R 755 /System/Library/Extensions/* && chown -R root:wheel /System/Library/Extensions/* && kextcache -system-caches.

- We got problem with USB ports (therefore, cannot install from USB). We fix it by:
  + First, Use `Clover Configurator` V4.39.1 app to mount EFI and patch ACPI (Look at "List of Patches" in Acpi menu  and apply All Of Them)
  + Install `USBInjectAll.kext` to inject all USB ports!

- HP Z420 crashes with many versions of FakeSMC and NullCPUPowerManagement.kext, so please **use those** in the repo!!!

- At first, when we don't have Nvidia WEB drivers, we need to disable NVidia kext by flag `nv_disable=1`. We later can install lastest Nvidia Web driver for 10.12.3
(https://images.nvidia.com/mac/pkg/367/WebDriver-367.15.10.35f01.pkg), and we will not need that flag anymore.

- Use SMBios of Mac Pro 5.1.

- The system cannot wake up after going sleep. We should set `Computer Sleep` to `Never` in System Preferences -> Energy Saver.

