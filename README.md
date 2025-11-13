# Introduction
<img width="608" height="299" alt="RK logo" src="https://github.com/user-attachments/assets/90ca562b-454c-4ab9-a1ba-7a427c989565" />

This repository is for the RK ROYAL KLUDGE RK918/RK919 US ANSI (or UK) layout firmware updater. If you're having any issues related to installing the wrong firmware on your board or need to rewrite/sniff the firmware, then this would help.
This firmware updater tool was sent by the engineers at rd02@rkgaming.com Huge thanks to them for successfully recovering my RK918


# DISCLAIMER
I am not responsible for any damage or bricking that occurs if this firmware is used on an incompatible keyboard. Use at your own risk.

As of 11/12/2025, I have extracted and uploaded the stock firmware .bin file for this keyboard. You can flash using the official SONiX USB MCU ISP Tool or use SonixQMK's Sonix Keyboard Flasher.

To flash QMK on this keyboard via Sonix Keyboard Flasher, set the MCU to SN32F24xB, and set the QMK offset to 0x00, as the SN32F24xB series has a ROM-based bootloader.

# Information
The RK918 and RK919 share the same PCB and features. The RK918 is a slight revision of the original RK919 PCB. If you take a look underneath the space bar of both keyboards, it will show "919 918 HFD", as shown below:

<img width="636" height="666" alt="image" src="https://github.com/user-attachments/assets/8bb99973-66c3-400c-9eeb-eae7a1ce5802" />

The MCU on these boards is a Huafenda HFD2201KBA, which is a rebranded Sonix SN32F248B microcontroller. These microcontrollers run off of the 32-bit ARM-Cortex M0 architecture. You can find the data sheet here: https://www.sonix.com.tw/article-en-4336-30356

The bootloader on these keyboards are unbrickable, as the bootloader on these chips are stored in ROM (Read-Only Memory) on the MCU. Even if you flash a completely incompatible firmware on the board, the keyboard will still light up partially in different areas or play a connect sound once you plug it in. There won't be a VID/PID dependng on what firmware you currently have installed on the keyboard.

<img width="729" height="218" alt="image" src="https://github.com/user-attachments/assets/e6767567-a077-451c-9f93-81fb6330a028" />

Both boards share the same Vendor ID/Product ID (0C45:8006), also used by older RK61 models.

The RK61 software can be used for lighting configurations on the RK918/RK919, though it lacks support for side lighting present on the RK918/RK919.

The name of the updater is "RK919_RGB Mechanical UK_V1.63_201107(2201)_With White Light Test_02_En" (translated). This firmware updater tool is meant for both US/UK layout keyboards, with no complications between the two layouts.


# Firmware update

Running the firmware updater regularly is a straightforward process.

1. Extract the file
2. Look for "RK919_RGB机械 UK_V1.63_201107(2201)_带白光测试_02_En.exe"
3. Open the updater
4. Press "Start"

The keyboard will start updating. You will notice the lighting on your keyboard completely dark besides the side lighting remaining at it's last state. Unplugging the keyboard will result in a keyboard stuck in bootloader mode until you reflash the firmware. This process usually takes about 15-30 seconds to update. I have speed up the recording to show the progress as shown below:

![HFDISP2025-10-0200-36-13online-video-cutter com-ezgif com-video-to-gif-converter](https://github.com/user-attachments/assets/2ae11d67-3fd7-499b-8af8-9f214698d62b)

<img width="572" height="205" alt="image" src="https://github.com/user-attachments/assets/e029aed9-ed3f-4f5e-9dc9-9e0e3e02279f" />


# Firmware update using ISP mode

<img width="542" height="293" alt="image" src="https://github.com/user-attachments/assets/34c22e54-d9d5-4ed8-acf6-4b0e433e74e9" />

In some cases, the firmware updater may fail to detect your keyboard. This is often due to a missing or incorrect VID/PID depending on the firmware currently installed, or in some cases, your keyboard isn't plugged in at all. *Please plug it in.* The firmware updater for most HFD keyboards only detect based off of VID (0c45). Luckily the RK918 features an In-System Programming (ISP) mode, which allows direct firmware flashing even when the updater does not detect the device automatically. The board requires 17 Philips head screws to disassemble the keyboard. One you've disassembled the board, you'll notice two chips. To determine the MCU location on the keyboard, it's typically the largest chip on the board. Any other chip may be an LED driver (HFD9901LIA). Next to the MCU, you will find two small pads.

<img width="678" height="915" alt="image" src="https://github.com/user-attachments/assets/19c3e355-4af0-4e87-a40b-88c3eb6daf6a" />

These pads are used to enter bootloader mode, which is important if the firmware updater tool cannot detect the keyboard. This is also important if you cannot get the keyboard to work at all. To use them:

With the keyboard unplugged, short the two pads using a bent paper clip or similar tool.

While keeping the pads shorted, plug in the keyboard.

If no lighting appears and the keyboard is detected with a VID/PID of 0C45:7040, then congratulations. You are now in bootloader mode. Safely remove the paper clip off of the pads.

Extract and run the firmware updater. Wait 15-30 seconds until you hear the disconnect/reconnect sound and see the keyboard powering on with side lighting and a ripple effect as shown below:

![RK918 boot compressed](https://github.com/user-attachments/assets/ca631e79-af68-4146-8e9c-036fecca397c)

Your keyboard is now restored and running its original firmware.
