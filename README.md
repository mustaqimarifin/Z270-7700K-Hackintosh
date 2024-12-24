<div align="center">
 <a href="https://arifin.xyz"
><img src="https://i.ibb.co/284vy3R/og-red.png" alt="og-red" width="200"></a>
 </a>
 <h1>arifin[xyz]</h1>

</div>

<div align="center">

<img src="./public/invisibleman.avifs" width=50 height=50/>
<img src="https://i.gifer.com/T3IX.gif" width=50 height=50/>

<h3>WELCOME BLUD</h3>

# macOS 14.7.2 Sonoma on Z270 using OpenCore 1.0.3

<p align="center">
<img width="128" src="img/sonoma.avif">
</p>

## Hardware

* Asus Strix Z270i
* Intel i7-7700K
* Intel HD 630
* \~AMD Radeon RX 580~
* Asus GTX 750Ti
* Audio Realtek ALC1220
* Ethernet Intel I219V7
* Wi-Fi + BT Wireless 8265 ( Taken from a broken laptop. This board comes with Atheros in most markets I believe.)
* Android Tethering using HoRNDIS
* 2 x Samsung 970 EVO (Dont recommend Samsung drives anymore)

## BIOS

* CSM: Disabled (mandatory)
* VT-d: Enabled
* Platform Power Management: Disabled
* XHCI Hand-Off: Enabled
* Network Stack: Disabled
* Wake on LAN: Disabled
* Initial Display Output: CPU Graphics
* Integrated Graphics: Enabled
* DVMT Pre-allocated: 1024MB
* Above 4G Decoding: Enabled
* CFG Lock: Disabled (mandatory)
* Fast Boot: Disabled
* OS Type: Windows 11
* Secure Boot: Disabled. Not worth enabling AT ALL if you're dual-booting Win 11. Microsoft always wants to take over the whole PC.

## What works well?

* RX580 worked well for years and died. Currently have my old 750Ti for Windows. Disabled in
  macOS with an SSDT and working framebuffer settings for iGPU with 2 displays
* Shutdown and restart
* Ethernet
* Sound ( Realtek and HDMI )
* USB ports (USB port map for this board)
* Wifi

## What's not working?

* Sleep: It's fake sleep because iGPU hacks are broken. It will just shut down and be greeted by an annoying system report upon reboot.
  Functional sleep requires an AMD GPU to be functional.

***

## ACPI

### DMAR/HPET/PLUG/XOSI/SBUS-MCHC/USB-Reset

Patched using SSDTTime from Windows

### SSDT-ECX.aml

USB Power settings and Fake EC (Laptop) because z270i has multiple EC's

### SSDT-NOVIDIA.aml

Disable GTX 750Ti for macOS

***

### Kexts

## Source the Kexts yourselves. Refer to config. Only USBModern and HoRNDIS provided in Kext folder

* Lilu 1.7.0
* NVMEFix 1.1.2
* Airportitlwm 2.3.0
* HibernationFixup 1.5.2
* BluetoolFixup 2.6.9
* IntelBluetoothFirmware 2.4.0
* IntelBTPatcher 2.4.0
* IntelMausi 1.0.8
* AppleALC 1.9.3
* AirportItlwm 2.3.0 - Sonoma14.4 Version!!
* WhateverGreen 1.3.7
* VirtualSMC 1.3.4 inc SMCProcessor + SMCSuperIO
* HoRNDIS 9.2 - Kext extracted from Official [HoRNDIS](https://github.com/jwise/HoRNDIS) Pkg

## USBModern.Kext

<p align="center">
<img width="128" src="img/usbmap.png">
</p>

While you can map from macOS, its annoying as hell. If you're needing to map from scratch best to do it in windows with
[USBToolBox](https://github.com/USBToolBox/tool).

It must be noted I was unable to use the kext produced by USBToolbox but the mapping was indeed correct. So I copied over the mapping on to a previous kext made with the OG [USBMap](https://github.com/corpnewt/USBMap) which you can refer to in the provided EFI

***

### config.plist

Been using SMBIOS iMac19,1 for a long time now. Works well. When i had my RX580 I was using iMacPro1,1 just for hardware DRM ( Netflix etc).

All attempts at hacking is solely your responsibility. Don't get mad at me if shit breaks LOL!
I hope this can serve as one of the many references for folks out there.

HAPPY HACKING
