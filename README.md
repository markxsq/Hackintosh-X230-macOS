# Hackintosh-X230
Clover and plist file for X230-K9V

Relevant specs of my X230: 
- CPU: i5-3230m
- SSD: Plextor PX-256M2M (APFS is used with trim set to 'on', no speed decreases noticed)
- Bluetooth: Broadcom BCM20702A0 (come with my x230 but need extra kext to work properly. In my case, BrcmPatchRAM2.kext and BrcmFirmwareData.kext from RehabMan/OS-X-BrcmPatchRAM are necessary. https://bitbucket.org/RehabMan/os-x-brcmpatchram info credit goes to /u/stormy90 on reddit https://www.reddit.com/r/hackintosh/comments/3t5bly/bluetooth_not_working_on_el_capitan_broadcom/ )
- WiFi dongle: Edimax EW-7611ULB (its bluetooth is invisible in macOS, or choose EW-7811Un for a WiFi only solution)

The files used for this hackintosh are mainly from xxx10101xxx on github - https://github.com/xxx10101xxx/ThinkPad-X230-macOS

The installation of macOS to x230 can be done with the typical vanilla approach:
1. Prepare a macOS (in this case, it's High Sierra) installation USB stick - https://hackintosher.com/guides/make-macos-flash-drive-installer/
2. Install Clover Bootloader to the USB stick, make sure you choose the USB stick as the destination and tick install to UEFI only - https://medium.com/@salbito/installing-clover-on-a-macos-sierra-installer-130705b91bfa
3. Copy and paste the files of this repository to EFI/Clover/ , to mount the EFI partition, use either Clover Configurator or command line with diskutil - http://osxdaily.com/2013/05/13/mount-unmount-drives-from-the-command-line-in-mac-os-x/
4. Generate a serial number with Clover Configurator, go to SMBIOS (on the left sidebar), hit 'Generate New' next to 'Serial Number' for whatever times you like. 
5. Generate a uuid, go to terminal, type 'uuidgen', hit 'enter', copy paste the results to the 'smUUID' on Clover Configurator. 
6. Copy 'Board Serial Number' to 'Rt Variables' - 'MLB', save the plist and quit Clover Configurator. 
7. Set BIOS as indicated in xxx10101xxx's repository. 
8. Boot into the USB stick, install 
Sierra - https://hackintosher.com/guides/macos-high-sierra-hackintosh-install-clover-walkthrough/
9. After the installation, install Clover Bootloader to the SSD/HDD of the macOS just installed, as what was did to the USB stick. 
10. Copy and Paste the EFI folder from the USB stick to the EFI paritition of the installed SSD/HDD. Now the macOS should be able to boot up with the USB stick. If not, don't panic, insert the USB stick and boot into the system installed see if there's anything wrong with the EFI partition and try again. 
11. Generate a SSDT for Power Management, follow the procedure suggested by Piker-Alpha - https://github.com/Piker-Alpha/ssdtPRGen.sh
12. Install WiFi dongle driver (in my case it's Edimax EW-7611ULB or EW-7811Un) - https://www.edimax.com/edimax/download/download/data/edimax/global/download/for_home/wireless_adapters/wireless_adapters_n150/ew-7611ulb
13. Done! 

Known issues:
1. d-sub output isn't working - not a news
2. trackpoint isn't working - both red dot and buttons, at chances they might work but not stable. Trackpad is working fine but nothing better than on windows (x230 users might have known what I'm talking about)
3. boot/awake animation glitch - minor stuff, but I wasn't able to fix it with the solution suggested by Bizzaro https://github.com/Bizzaro/x230-osx . If anyone knows how to fix it please share the solution. Thanks. 
4. Backlight brightness is set to maximum at boot. In my case this is due to Clover Bootloader overwrite NVRAM's value at boot. It uses Backlight Level: 0xFFFF at boot, this can be check by going to 'Options' - 'Graphics Injector' in Clover Bootloader in the middle of booting. The brightness stays at the previous value before rebooting if '0xFFFF' is deleted, but I seem can't find a way to set empty as default. If anyone knows how to do it, please share it with me. Thanks. 

Hope the info can be helpful for anyone who'd like to install macOS on x230. 
