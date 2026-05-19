# unic-projector-uc68
This project is the Chinese unic uc68 clone projector, I tried to debug and fix its error file system. 
This is a Chinese "UNIC" projector clone with "40-Main-V1.0 (20181228)" motherboard.

With the help of artificial intelligence, it was possible to find out the location of the debug port on this type of motherboard, and with a ch340 serial uart device, it was possible to extract information about the cause of the error in my projector.


Warning: everyone should modify the firmware only at their own risk, and make sure to back up the faulty firmware before making any changes! Recommended with CH341 flash programmer.


And it is very important to program in 3.3 volt mode, because in 5 volt mode we will destroy the flash chip!


And because I experienced that it cannot be detected when soldered, it must be soldered from the factory PCB to a programming PCB! It is not possible to program with "SOIC8 SOP8 Test Clip Flash IC Clips".


The VGA connector pin 10 is the GND, pin 12 is the RX, pin 15 is the TX data pin, but it is important that it has 3.3 volt TTL levels. I have attached a picture of this pinout here.(pinout.png)

The uart connector (VGA) must be connected with a baud rate of 115200.

I let the startup run and looked at what error messages I got at startup, which revealed the "SQUASHFS error".

I entered the "Realtek>" state with the ESC key, where I didn't do anything, but maybe it's still useful to someone.

In the dump I saved (uc68-dump.bin), the file system is faulty and it says "SQUASHFS error: xz_dec_run error, data probably corrupt" when starting.

The other firmware is a flash dump downloaded from 4pda.to (unic_uc68_4pda.bin), where the HDMI and VGA ports did not work for me. I changed the name of the 4PDA.to firmware, but the file is the original one.

I saved and flashed from the 25Q128 flash (25VG128ASEG) using the CH341A programmer.

I created a hybrid firmware version with artificial intelligence from the two firmware.bins and I'm trying to bring a fixed version to life with the right settings and a working SQUASHFS.
This resulted in the attached fixed.bin file. 

//

Comment:
With this linux command: dd if=unic_uc68_4pda.bin of=fixed.bin bs=1 skip=$((0x003F1FCE)) seek=$((0x003F1FCE)) conv=notrunc

The fixed.bin here is the original firmware (uc68-dump.bin) renamed and overwritten with this command, which is part of the flash.

//

My hardware:  Realtek RTD2936HBZ CPU ,realtek rtl8188ETV wifi module ,U-Boot 2012.07 ,LC03502G24E LCoS (Liquid Crystal on Silicon) And theoretically the display : "PANEL_TYPE=duowei_800_480"



The problem with my projector is that it is not an original UNIC uc68, so I cannot load the display panel settings, but those who have an original UNIC uc68 projector can use the original file that I found for it. 

I have attached my system startup in the bootlog.txt file.

My current error is "DCC_bin_boundary_flag=1" because the color management does not work.


An interesting error from the past of LG TV's firmware: "[uboot] SI2151_DBG: xTuner_I2C_Write: error" and there is no TV tuner in this projector.

Google Gemini analyzed the files and came to this conclusion:

"The Chinese manufacturer took a firmware originally developed for LG TVs (probably webOS-based or Android with the Realtek chip used by LG) and tried to "weld" it onto its own, cheaper Duowei 800x480 display."


The firmware uses these as default panel settings. "INX8903_i2c_cmd , LT8911_Initial , LG_ART4_EPI_PANEL_Script"
therefore, it is likely that this was the firmware of an LG TV originally.
