How to install MacOS Sierra 10.12.3 on HP Z420 Workstation.

Overall, we will use Unibeast to create a USB Installer.

From my Mac OS X 10.10 Yosemite. We download the Mac OS Sierra Installer (go to App Store to download).

Then, we use the lastest Unibeast (UniBeast 7.0.1) to create a bootable USB. However, we have to use kexts from CustoMac Essential package and put these kexts to /EFI/CLOVER/kexts/Other/ directory.

### Here the Tricks 

Note: I also put my `/Volumes/EFI/EFI/CLOVER` directory and all kexts we need in the repo.

- Install the lastest version of CLOVER (e.g., v2k4)

- We have to use flag `npci=0x2000` all the time.  (I also use `dart=1` also)

- Z420 have problem of running the Installer (crash randomly), we can fix that with flag `cpus=1`. However, this make our PC slow, therefore, We fix this problem by installing the kext `VoodooTSCSync.kext` at `/System/Library/Extensions` .  Remember to fix permission.  E.g.    

     chmod -R 755 /System/Library/Extensions/* && chown -R root:wheel /System/Library/Extensions/* && kextcache -system-caches.

- We got problem with USB ports (therefore, cannot install from USB). We fix it by:
  + First, Use `Clover Configurator` V4.39.1 app to mount EFI and patch ACPI (Look at "List of Patches" in Acpi menu  and apply All Of Them)
  + Install `USBInjectAll.kext` to inject all USB ports!

- HP Z420 crashed with many versions of FakeSMC and NullCPUPowerManagement.kext, so please use those in the repo!

- At first (when we don't have Nvidia WEB drivers), we need to disable NVidia kext by flag `nv_disable=1`. After, we install lastest Nvidia Web driver for 10.12.3
(https://images.nvidia.com/mac/pkg/367/WebDriver-367.15.10.35f01.pkg), you will not need that flag anymore.

- Use SMBios of Mac Pro 5.1.

- The system cannot wake up after going sleep. We should set `Computer Sleep` to `Never` in System Preferences -> Energy Saver.

