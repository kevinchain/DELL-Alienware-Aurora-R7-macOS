# DELL-Alienware-Aurora-R6/R7/R8-macOS (Mojave, 10.14.x)
Full working macOS for DELL Alienware Aurora R6/R7/R8. 

There may still exist some issues in this configuration, if you have any problem or improvement, you can share it through submitting an issue.

# Update log

**2019/01/22** 
    
Add usb port limited patch, you can choose to use this patch or the customed SSDT patch.

This following patchs allow root hub port limit over 0xf to 0x3f.

Comment: USB port limit patch 10.14.1 10.14.2 (credit ydeng).   
Name: IOUSBHostFamily  
Find: 00e0 83fb 0f0f 8716 0400  
Replace: 00e0 83fb 3f0f 8716 0400   

Comment: USB Port limit patch 10.14.1, 10.14.2.   
Name: com.apple.driver.usb.AppleUSBXHCI  
Find: 00 00 83 FB 0F 0F 83 8F 04 00 00  
Replace: 00 00 83 FB 3F 0F 83 8F 04 00 00  

**2018/12/05**

Update my machine's MacOS to 10.14.2 successfully with this EFI settings.

**2018/11/22**

Update SSDT for USBInjectAll.kext, USB3 ports can now run at 5Gb/s. I do not have USB-C decives, so the two USB-C ports are not injected, you can modify ssdt by yourself to inject them.
> <font size="2">add: /EFI/CLOVER/ACPI/patched/SSDT-UIAC.aml    
> update: /EFI/CLOVER/config.plist</font>

**2018/11/18**  

Update to Mojave 10.14.x, The configuration and files for High Serria are moved to directory High-Serria-10.13.6**. 

Remove Nvidia Webdrive, replace Nvidia card by AMD card (RX 480,580,470,570,VEGA56, VEGA64, etc.). 

Replace SMBIOS imac 14,1 by macmini 8,1. mac mini 2018 natively support the 8th generation Intel cpu and UHD 630 graphics card. 

Remove HWPEnabler.kext. 

Add some useful tools.  



# Hardware
This clover setting should work for recent Alienware Aurora R6/R7/R8 desktops  (released on 2017 and 2018) which installed with Intel CPU and Nvidia GPU. It may need some minor modifications to completely fulfill your machine.

The hardware details for my machine: Aurora R7 with i7-8700, ~~GTX 1080~~, 32GB memory, MSI RX 580, Adata sx8200 480g nvme ssd, DW1830 wifi+bluetooth card

# Working condition
I connect two 4k monitors to the machine both through display port on RX 580, they work good. 

FaceTime and IMessage work good.

Bluetooth works good.

Airdrop works good.

Sleep and wake are good.

Usb ports are injected through SSDT-UIUC.aml

Intel integrated GPU UHD 630 is natively supported by Mojave when using macmini 8,1. 

I have no related devices, so I did not test USB-C ports and HDMI ports. 

Killer 1535 Wifi+bluetooth card does not work (need to be replaced).

Magic mouse and Trackpad work good.

# Issues
~~There is no suitable patches now, USB3 works on 480 M/s (Mojave 10.14.2)~~
Already fixed by adding SSDT for USBInjectAll.kext, USB3 ports can now run at 5Gb/s. See update log for details.   

For the USB problem, please not plug to the first one from left of the 4 usb3 ports in the back. These is no workable 15 port limit patch for Mojave now, therefore only less than 15 port are inject through SSDT. These injected ports include all the four ports in the front, the four usb2 ports in the second line in the back, and the 3 usb3 ports (except the first one from left) in the back.

The first one from left usb3 port in the back is indeed a usb 3.1 port, and controlled by a usb hub. While other usb3 ports are controlled by the motherboard.

# Installation

1. Following the general installation tutorial to install macOS. (Note that, you may need to update the EFI/clover in your USB installer to the latest version, and copy paste all of my EFI files, then try to install MacOS. The default EFI/clover version created by UniBeast is a bit old.)

2. Install the bluetooth drive for DW1830 (BrcmPatchRAM) 
    Copy kexts in directory bluetooth to /System/Library/Exetensions

3. Use Kext Utility to update cache for kexts, you can find this tool in directory tools

4. Replace the default EFI by this one.

5. Setting Audio: Try to plug in your audio device to the centre connector in the second row and select Internal speakers in System Preferences>Sound





