# Hackintosh Optiplex 3070 with with Monterey 12.6.7

My EFI Folder using clover OpenClover 1.0.0

Runinng perfect lan, video, sensors, icloud, etc, except Audio on board.(yet). I use Usb Audio Speakers, so its fine for me.

![about_this_mac](/repository_media/about_monterey.png)
![dual_monitor](/repository_media/dual_monitors.png)

[Hardware list](./repository_media/hardware_list.txt) created with [OCSysInfo](https://github.com/KernelWanderers/OCSysInfo)

## How to Use

This is the final EFI Folder after 1 week of lot of tests, a lot of reboots. 

This is a stable version of the Opencore settings 1.0.0 needed to boot install and use OSX Monterey for this MICRO ATX computer.

Don't just grab that EFI folder without understanding what you're doing.
The process of running OSX on a PC using OpenCore requires knowledge of your hardware, how drivers are injected and how Opencore provides the necessary bridge for Mac OS to work on customized machines. The testing process and many reboots is a very rich learning to be able to solve problems in case of OSX or Opencore updates.

You can :
1 - Create a pendrive or an EFI partition using the clone of this project with only the EFI folder in the root of the partition and check if an image created from a mac OSX installation of Catalina, Big Sur or Monterey can boot in the case of Monterey an image created [using](https://support.apple.com/pt-br/HT201372)

```sh
sudo /Applications/Install\ macOS\ Monterey.app/Contents/Resources/createinstallmedia --volume /Volumes/MyVolume
```

And before testing, correct the snippet of the config.plist file using [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) to generate your values. A good explanation is described [here](https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html#using-gensmbios) 

**DON'T USE THE VALUES IN THIS REPOSITORY FOR YOU, PLEASE GENERATE YOURS**

```xml
	<key>PlatformInfo</key>
	<dict>
		<key>Automatic</key>
		<true/>
		<key>CustomMemory</key>
		<false/>
		<key>Generic</key>
		<dict>
			<key>AdviseFeatures</key>
			<false/>
			<key>MaxBIOSVersion</key>
			<false/>
			<key>MLB</key>
			<string>USE_GenSMBIOS_AND_SET_YOURS</string>
			<key>ProcessorType</key>
			<integer>0</integer>
			<key>ROM</key>
			<data>USE_GenSMBIOS_AND_SET_YOURS</data>
			<key>SpoofVendor</key>
			<true/>
			<key>SystemMemoryStatus</key>
			<string>Auto</string>
			<key>SystemProductName</key>
			<string>iMac19,1</string>
			<key>SystemSerialNumber</key>
			<string>USE_GenSMBIOS_AND_SET_YOURS</string>
			<key>SystemUUID</key>
			<string>USE_GenSMBIOS_AND_SET_YOURS</string>
		</dict>
```

OBS: The `iMac19,1` is the Architecture model to run OSX Monterey on this computer.

Check https://dortania.github.io/OpenCore-Install-Guide/extras/smbios-support.html#how-to-decide

Good luck, patience, It may be work, but it's worth it.

**Important**

## BIOS Settings
- General → Advanced Boot Options: uncheck 
- System Configuration → SATA Operation: AHCI 
- Secure Boot → Secure Boot Enable: Disabled 
- Intel® Software Guard Extensions™ → Intel® SGX™ Enable: Disabled 
- Power Management → Block Sleep: uncheck 
- Virtualization Support → VT for Direct I/O: uncheck

My Suggestion  
Download the latest version of OpenCore-debug and RTFM (read the docs) [here](https://dortania.github.io/OpenCore-Install-Guide/prerequisites.html)

Start with docs following step by step to configure your config.plist with ProperTree.

Use this EFI folder as bkp or create a Linux Pen drive to boot the machine, if necessary fix the Efi folder in case of Kernel Panic on reboot.

I left the entire history in git of step by step in this repository to "educational purposes"
![git_history](/repository_media/git_history.png)


