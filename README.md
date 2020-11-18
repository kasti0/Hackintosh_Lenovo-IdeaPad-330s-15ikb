# Hackintosh_Lenovo-IdeaPad-330s-15ikb

A short discription how to set up macOS on the Lenovo Ideapad 330s-15ikb 81F5. If your Lenovo IdeaPad or laptop in general is slightly different this setup or parts of it may not work for you! Please don´t blindly copy-paste everything.
Follow the vanilla OpenCore guide by Dortania to set everything up:
https://dortania.github.io/OpenCore-Install-Guide/

*DISCLAIMER: Most of the Kexts and ACPI files which are used for this project are pre-built and it´s not my intention to take fales credit for them. I try to link to all original files and creators or guides where I took them from.*

*Note: Files marked with a (e) are essential for booting, all other are providing extra functionality or fixing issues.*



# Information:

### Hardware

  - Lenovo Ideapad 330s-15ikb 81F5
  - CPU: Intel i5-8250U (KabyLake-R)
  - iGPU: UHD620 (KabyLake-R)
  - Disk 1: 512GB WD NVMe
  - (added) Disk 2: 512GB sATA SSD (for Windows)
  - (added) Wifi/BT-Card: BCM94352Z (Lenovo branded)
  
  
### Software (as of 17/11/2020):
  - macOS Big Sur 11.0.1
  - OpenCore 0.6.4
  - all used kexts up-to-date
  
  
### Feature status:
  - ~~external displays connected via HDMI are not recognized after wake from sleep/ reboot, need to re-plug cable (help appreciated)~~ fixed by adding "force-online" under DeviceProperties>Add>PciRoot(0x0)/Pci(0x2,0x0)
  - Wifi, Bluetooth, Airdrop, SideCar, Sleep, Wake, iGPU acceleration etc. all working
  - no non-working features known (please open an issue if you find any)
  
  
  
# Used

### Guides:
  - Dortania OpenCore guide for Vanilla macOS/ Hackintosh setup: https://dortania.github.io/OpenCore-Install-Guide/
  - RehabMan DSDT patching for working battery status: https://www.tonymacx86.com/threads/guide-how-to-patch-dsdt-for-working-battery-status.116102/
  - WEG Framebuffer patching: https://github.com/acidanthera/WhateverGreen/blob/master/Manual/FAQ.IntelHD.en.md


### Tools:
  - SSDTTime: https://github.com/corpnewt/SSDTTime
  - USBMap: https://github.com/corpnewt/USBMap
  - Hackintool: https://github.com/headkaze/Hackintool
  - ProperTree: https://github.com/corpnewt/ProperTree
  - gibMacOS: https://github.com/corpnewt/gibMacOS
  


# Setup

### BIOS

 - Configuration> Intel Virtual Technology: Disabled
 - Configuration> Storage> Controller Mode: AHCI mode
 - Security> Intel Platform Trust Technology: Disbaled
 - Security> Secure Boot: Disbaled
 - Boot> Boot Mode: UEFI (should already be UEFI, just to be sure)
 - Boot> USB Boot: Enabled
 -> everything else can be left default
 
 
### SMBIOS

 - refer to this guide for more information: https://dortania.github.io/OpenCore-Install-Guide/config-laptop.plist/kaby-lake.html#platforminfo
 - for this setup the SMBIOS of the MacBookPro15,2 with i5-8259U is used, as it´s the closest we can match the i5-8250U of the Ideapad (https://everymac.com/systems/apple/macbook_pro/specs/macbook-pro-core-i5-2.3-13-mid-2018-true-tone-display-touch-bar-specs.html)
 - according to the Dortania guide a MacBookPro14,X is better, feel free to try and use those SMBIOS and see if it gets you better results


### config.plist
 - the config.plist is the exact result of follwing the Dortania guide for Kabylake laptops: https://dortania.github.io/OpenCore-Install-Guide/config-laptop.plist/kaby-lake.html#starting-point


### Files

#### ACPI
  
| Name       | Description           |Source|
| ------------- |-------------|-------------|
| SSDT-BAT0      | for battary/ charging status |slef, with RehabMan DSDT/SSDT-hotpatch guide |
| SSDT-EC-USBX (e)      |  fake EC device and manag USB power settings   |created with SSDTTime, https://dortania.github.io/Getting-Started-With-ACPI/Universal/ec-fix.html |
| SSDT-GPI0 |    for working trackpad   | https://dortania.github.io/Getting-Started-With-ACPI/Laptops/trackpad-methods/manual.html|
| SSDT-GPRW | fixing sleep issues      | https://dortania.github.io/OpenCore-Post-Install/usb/misc/instant-wake.html| 
| SSDT-HPET (e) |  fixing IRQ conflicts      | created with SSDTTime|
| SSDT-LID |   making sleep on lid-close work    | self |
| SSDT-PLUG |  for CPU managment      |created with SSDTTime, https://dortania.github.io/Getting-Started-With-ACPI/Universal/plug.html |
| SSDT-PNLF |   for backlight adjustment    |https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-PNLF.aml |
| SSDT-Q0A_QC9 |  dirty work around for fixing ACPI errors with thes methods, still need to find out what they are sued for     | self|
|SSDT-SBUS-MCHC  | make the SMBus work for better combatibility      | https://dortania.github.io/Getting-Started-With-ACPI/Universal/smbus.html|
| SSDT-XOSI (e) |       |https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-XOSI.aml |
 
 
    
 
#### Kext
*Note: Kexts won´t be updated on a regular basis or not at all. Please use the provided links or hackintool to manually update kexts. DO NOT use hackintools method to install kexts. Just download them and copy-paste new versions in to your OC/KEXT/ folder.*
   
| Name       | Description           |Source|
| ------------- |-------------|-------------|
|   AirportBcrmFixup   | for WIFI on non-native WIFI cards         |https://github.com/acidanthera/AirportBrcmFixup |
|   BrcmPatchRam + Plugins   | uploading Bluetooth firmware       |https://github.com/acidanthera/BrcmPatchRAM |
|   CPUFriend (+ CPUFriendDataProvider)   |  more detailed power managment, to create the DataProvider kext follow the instructions in the source link        |https://dortania.github.io/OpenCore-Post-Install/universal/pm.html#using-cpu-friend |
|   NoTouchID   |   disbale ToichID-check for faster authorization       |https://github.com/al3xtjames/NoTouchID |
| NVMeFix     |   different patches for non-Apple SSDs       | https://github.com/acidanthera/NVMeFix|
|  VirtaulSMC + Plugins (e)    |  for sensor reading        | https://github.com/acidanthera/VirtualSMC|
| USBPorts     | mapping the USB ports         |created with USBMap tool |
| VoodooI2C + Plugins     | trackpad         |https://github.com/VoodooI2C/VoodooI2C |
|  VoodooPS2    |   keyboard       |https://github.com/acidanthera/VoodooPS2 |
|  WhateverGreen (e)    | framebuffer patching for iGPU and display ports         | https://github.com/acidanthera/WhateverGreen|

   
 
