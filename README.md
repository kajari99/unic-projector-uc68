# unic-projector-uc68
This project is the Chinese unic uc68 clone projector, I tried to debug and fix its error file system. 
This is a Chinese "UNIC" projector clone with "40-Main-V1.0 (20181228)" motherboard.

With the help of artificial intelligence, it was possible to find out the location of the debug port on this type of motherboard, and with a ch340 serial uart device, it was possible to extract information about the cause of the error in my projector.


The VGA connector pin 10 is the GND, pin 12 is the RX, pin 15 is the TX data pin, but it is important that it has 3.3 volt TTL levels. I have attached a picture of this pinout here.(pinout.png)

The uart connector (VGA) must be connected with a baud rate of 115200.

I let the startup run and looked at what error messages I got at startup, which revealed the "SQUASHFS error".

I entered the "Realtek>" state with the ESC key, where I didn't do anything, but maybe it's still useful to someone.

In the dump I saved (uc68-dump.bin), the file system is faulty and it says "SQUASHFS error: xz_dec_run error, data probably corrupt" when starting.

The other firmware is a flash dump downloaded from 4pda.to (unic_uc68_4pda.bin), where the HDMI and VGA ports did not work for me.

I saved and flashed from the 25Q128 flash (25VG128ASEG) using the CH341A programmer.


My hardware:  Realtek RTD2936HBZ CPU ,realtek rtl8188ETV wifi module ,U-Boot 2012.07 ,LC03502G24E  LC3502 LCoS (Liquid Crystal on Silicon)


The problem with my projector is that it is not an original UNIC uc68, so I cannot load the display panel settings, but those who have an original UNIC uc68 projector can use the original file that I found for it. My other problem is that the CRC (Cyclic Redundancy Check)  of my penel.bin file is not correct for my system.And I also experienced a DCC (Dynamic Color Control) error because of it.
