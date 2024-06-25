# Hackintosh for Lenovo ThinkPad E580

![Lenovo ThinkPad E580](image.png)

OpenCore configuration for my main laptop. Currently runs macOS Sonoma but planning to upgrade it to macOS Sequoia once it's stable and itlwm works on it.

I strongly recommend you to use rEFInd when you want to dual boot. Booting Windows through Bootcamp has been only problematic.

If you're planning to use this, I recommend you check the Dortania OpenCore guide first to fix things like language, iServices and keyboard layout.

## Specs
- CPU: Intel Core i5-8250U (8 cores, 16 threads)
- GPU: Intel UHD Graphics 620 (dGPU is not supported, see later)
- RAM: 8GB DDR4
- Storage: I use a SATA SSD and leave my NVMe for Windows, but it should work on both.
- Ethernet: RTL8111/8168/8411
- Wi-Fi: Intel 3165AC+BT (supported by itlwm)

## What works
- HDMI video out + audio out
- USB ports
- 3.5mm audio jack (haven't tried microphone yet)
- Keyboard
- Webcam
- Integrated speakers and microphone
- Ethernet
- Trackpad
- Function keys
- Wi-Fi and Bluetooth

## What doesn't work
- dGPU if you have one
- AirDrop and related services because of limited Intel wireless card support, can be fixed by replacing.
- Touch ID

## Known issues
- HDMI doesn't work when booting up while HDMI is plugged in (must be plugged in while booting up)
- Function keys stop working after waking from sleep
- On Sonoma, Bluetooth is not 100% reliable.

## If you have dGPU ...
... add this to your `boot-args` to disable it: `-wegnoegpu`. It's not supported by macOS.

## How to use
You need:

1. a USB stick with atleast 16GB of storage
2. Lenovo ThinkPad E580
4. a Mac/Mac VM to make the installer

Step 1: Get macOS onto your USB stick. You can do this [using another macOS system](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/mac-install.html). You cannot get that result on Windows or Linux yet, unless you use a macOS VM, which I won't get into.

Step 2: Use [MountEFI](https://github.com/corpnewt/MountEFI) to mount your bootable USB's EFI partition, and copy the EFI folder to it.

Step 3: Plug the USB into the laptop and when you see the Lenovo logo press Enter to interrupt normal boot. Open UEFI setup and make sure Secure Boot and Fast Boot is disabled. Leave after.

Step 4: Press F12 during the Lenovo logo and select your USB stick.

Step 5: Go through the installer and follow the instructions.

Step 6: Once the installer is done, you still need to move the USB's EFI folder to your SSD's EFI partition. Use OpenCore Configurator for that.

And that's it!