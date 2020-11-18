# Hackintosh_Lenovo-IdeaPad-330s-15ikb
A short discription how to set up macOS on the Lenovo Ideapad 330s-15ikb 81F5.
Follow the vanilla OpenCore guide by Dortania to set everything up:
https://dortania.github.io/OpenCore-Install-Guide/

*DISCLAIMER: Most of the Kexts and ACPI files which are used for this project are pre-built and it´s not my intention to take fales credit for them. I try to link to all original files and creators or guides where I took them from.

*Note: Files marked with a (e) are essential for booting, all other are providing extra functionality or fixing issues.


# Information:

## Hardware

  - Lenovo Ideapad 330s-15ikb 81F5
  - CPU: Intel i5-8250U (KabyLake-R)
  - iGPU: UHD620 (KabyLake-R)
  - Disk 1: 512GB WD NVMe
  - (added) Disk 2: 512GB sATA SSD (for Windows)
  - (added) Wifi/BT-Card: BCM94352Z (Lenovo branded)
  
  
## Software (as of 17/11/2020):
  - macOS Big Sur 11.0.1
  - OpenCore 0.6.4
  - all used kexts up-to-date
  
## Feature status:
  - ~~external displays connected via HDMI are not recognized after wake from sleep/ reboot, need to re-plug cable (help appreciated)~~ fixed by adding "force-online" under DeviceProperties>Add>PciRoot(0x0)/Pci(0x2,0x0)
  - Wifi, Bluetooth, Airdrop, SideCar, Sleep, Wake, iGPU acceleration etc. all working
  - no non-working features known (please open an issue if you find any)
  
# Used

## Guides:
  - Dortania OpenCore guide for Vanilla macOS/ Hackintosh setup: https://dortania.github.io/OpenCore-Install-Guide/
  - RehabMan DSDT patching for working battery status: https://www.tonymacx86.com/threads/guide-how-to-patch-dsdt-for-working-battery-status.116102/
  - WEG Framebuffer patching: https://github.com/acidanthera/WhateverGreen/blob/master/Manual/FAQ.IntelHD.en.md

## Tools:
  - SSDTTime: https://github.com/corpnewt/SSDTTime
  - USBMap: https://github.com/corpnewt/USBMap
  - Hackintool: https://github.com/headkaze/Hackintool
  - ProperTree: https://github.com/corpnewt/ProperTree
  - gibMacOS: https://github.com/corpnewt/gibMacOS
  
# Files
  
  
  ACPI:
  
   - SSDT-BAT0: for battary/ charging status
   - SSDT-EC-USBX (e): (created with SSDTTime) (https://dortania.github.io/Getting-Started-With-ACPI/Universal/ec-fix.html)
   - SSDT-GPI0: for working trackpad (https://dortania.github.io/Getting-Started-With-ACPI/Laptops/trackpad-methods/manual.html)
   - SSDT-GPRW: fixing sleep issues (https://dortania.github.io/OpenCore-Post-Install/usb/misc/instant-wake.html)
   - SSDT-HPET (e): fixing IRQ conflicts (created with SSDTTime) (https://dortania.github.io/Getting-Started-With-ACPI/Universal/irq.html)
   - SSDT-LID: making sleep on lid-close work
   - SSDT-PLUG: for CPU managment (created with SSDTTime) (https://dortania.github.io/Getting-Started-With-ACPI/Universal/plug.html)
   - SSDT-PNLF: for backlight adjustment (https://dortania.github.io/Getting-Started-With-ACPI/ssdt-methods/ssdt-prebuilt.html#laptop-skylake-and-kaby-lake)
   - SSDT-Q0A_QC9: dirty work around for fixing ACPI errors with thes methods, still need to find out what they are sued for
   - SSDT-SBUS-MCHC: make the SMBus work for better combatibility (https://dortania.github.io/Getting-Started-With-ACPI/Universal/smbus.html)
   - SSDT-XOSI (e): (https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-XOSI.aml)
    
 
   Kext:
   
   - AirportBcrmFixup + Brcm: for Wifi and Bluetooth
   - BrightnessKeys: change brightness with F11/F12 key
   - CPUFriend + DataProvider: more detailed power managment (https://dortania.github.io/OpenCore-Post-Install/universal/pm.html#using-cpu-friend)
   - NoTouchID: disbale ToichID-check for faster authorization
   - NVMeFix: different patches for non-Apple SSDs
   - VirtaulSMC + Plugins (e): for sensor reading
   - USBPorts: mapping the USB ports
   - VoodooI2C + Plugins: trackpad
   - VoodooPS2: keyboard
   - WhateverGreen (e): framebuffer patching for iGPU and display ports
