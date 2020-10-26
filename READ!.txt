This is a project of AVR Atmega fusebit doctor (HVPP+HVSP).

Hardware and software: Manekinen (Pawe³ Kisielewski)
manekinen@gmail.com

Compiler: bascom v.1.11.9.0   

PCB: Eagle light v.5.4.0        

Project website:  http://diy.elektroda.eu/atmega-fusebit-doctor-hvpp/
English language: http://diy.elektroda.eu/atmega-fusebit-doctor-hvpp/?lang=en

Any modifications allowed, do not remove this README! from archive.
Do not remove info from pcb and code.

Any usage of this project in commercial/profit purposes is prohibited.

Have a question? Post in comments on site, or contact me at manekinen@gmail.com

For software updates notifications, follow me at http://www.twitter.com/manekinen


03.05.2010

*******************************************************************************
*******************************************************************************

SUPPORTED CHIPS LIST (from v2.09) 145:

1kB:
AT90s1200, Attiny11, Attiny12, Attiny13/A, Attiny15
2kB:
Attiny2313/A, Attiny24/A, Attiny26, Attiny261/A, Attiny28, AT90s2333, Attiny22, Attiny25, AT90s2313, AT90s2323, AT90s2343
4kB:
Atmega48/A, Atmega48P/PA, Attiny461/A, Attiny43U, Attiny4313, Attiny44/A, Attiny48, AT90s4433, AT90s4414, AT90s4434, Attiny45
8kB:
Atmega8515, Atmega8535, Atmega8/A, Atmega88/A, Atmega88P/PA, AT90pwm1, AT90pwm2, AT90pwm2B, AT90pwm3, AT90pwm3B, AT90pwm81, AT90usb82, Attiny84, Attiny85, Attiny861/A, Attiny87, Attiny88, AT90s8515, AT90s8535
16kB:
Atmega16/A, Atmega16U2, Atmega16U4, Atmega16M1, Atmega161, Atmega162, Atmega163, Atmega164A, Atmega164P/PA, Atmega165A/P/PA, Atmega168/A, Atmega168P/PA, Atmega169A/PA, Attiny167, AT90pwm216, AT90pwm316, AT90usb162
32kB:
Atmega32/A, Atmega32C1, Atmega323/A, Atmega32U2, Atmega32U4, Atmega32U6, Atmega32M1, Atmega324A, Atmega324P, Atmega324PA, Atmega325, Atmega3250, Atmega325A/PA, Atmega3250A/PA, Atmega328, Atmega328P, Atmega329, Atmega3290, Atmega329A/PA, Atmega3290A/PA, AT90can32
64kB:
Atmega64/A, Atmega64C1, Atmega64M1, Atmega649, Atmega6490, Atmega649A/P, Atmega6490A/P, Atmega640, Atmega644/A, Atmega644P/PA, Atmega645, Atmega645A/P, Atmega6450, Atmega6450A/P, AT90usb646, AT90usb647, AT90can64
128kB:
Atmega103, Atmega128/A, Atmega1280, Atmega1281, Atmega1284, Atmega1284P, AT90usb1286, AT90usb1287, AT90can128
256kB:
Atmega2560, Atmega2561

*******************************************************************************
*******************************************************************************

CHANGELOG:

________________________
First release 03.05.2010

Hardware 2.0c PCB
-first PCB - BUGGED - DO NOT CLONE!

Firmware 2.0g BETA:
-first public release
-support only Atmega8, Atmega16, Atmega32
FUSEBITS: internal 8MHz clock, EESAVE enabled ( L:0xE4 H:0xD1 )

____________________
#1 UPDATE 15.05.2010

Hardware 2.0d PCB:
-fixed reset line issues - added 1K pulldown resistor

Firmware 2.01 BETA:
-added support for 73 chips, total 76
FUSEBITS: internal 8MHz clock, EESAVE enabled ( L:0xE4 H:0xD1 )


____________________
#2 UPDATE 03.06.2010

Hardware adapters:
-"#1 adapter" as HVPP extension, for 20pin Attiny26 compatible and 40pin Atmega8515 compatible processors.
-"HVSP adapter" for 8pin and 14pin HVSP processors.

Firmware 2.03:
-added support for HVPP chips: AT90s8515, AT90s8535, AT90s1200, AT90s4433, AT90s4414, AT90s4434, AT90s2333
-added support for HVSP adapter and HVSP chips: (8pin) Attiny11, Attiny12, Attiny13, Attiny15, Attiny25, Attiny45, Attiny85, Attiny22, AT90s2323, AT90s2343 (and 14pin) Attiny24, Attiny44, Attiny84
-device will automatically detect the HVSP adapter and start in the HVSP mode (info on rs232 output).
FUSEBITS: internal 8MHz clock, EESAVE enabled ( L:0xE4 H:0xD1 )

Other:
-added all sockets compatibility list with images... "B" means that this is the adapter #1 socket, and "C" - HVSP adapter socket.
-total supported chips: 96, total DIL socket compatible: 53.
-as this is now 2in1 (HVPP and HVSP) 8kB of Atmega8 memory was too short to fit all the goods inside...
-not all of chips names are send over rs232, but most common. This does not affect fixing process in any way.
-some of text for rs232 are holded in the eeprom memory. Even if you do not need the rs232 output, you MUST write the EEP.BIN

____________________
#3 UPDATE 31.07.2010

Firmware 2.04:
-fixed couple of bugs
-added new processors support, total 106 (138)
-internal clock change to 1MHz, budrate on UART output change to 2400bps
ATTENTION, FUSEBITS! If you make an update of firmware to 2.04, please change the internal clock generator to 1MHz.
If you make this circuit from beginning, just set the EESAVE fusebit – 1MHz clock is already set as default.
FUSEBITS: internal 1MHz clock, EESAVE enabled ( L:0xE1 H:0xD1 )

____________________
#4 UPDATE 18.08.2010

Firmware 2.05:
-no eeprom file needed
-improved support for 20-pin chips
-improved signature recognition
-fixed attiny26 issues
-no chip names trough uart
-uart baudrate 4800 (2400 was just too slow)
FUSEBITS: internal 1MHz clock, EESAVE enabled ( L:0xE1 H:0xD1 )

____________________
#5 UPDATE 07.11.2010

Firmware 2.06:
-fixed Atmega324P signature recognition
-added proper timings for Attiny15 on PB.3
-fixed data bug in hvsp "chip erase" command
-added proper additional data for Attiny15 "chip erase" command
FUSEBITS: internal 1MHz clock, EESAVE enabled ( L:0xE1 H:0xD1 )

____________________
#6 UPDATE 27.11.2010

Hardware: Added a SMD version of PCB - by Shuffle (thanks!)
-"doctor" part as smd
-dip sockets part as a adapter
-added usb (tf232 chip)

Check the "SMD-pcb" folder, added only necessary files.
To get original package from Shuffle (with pictures), go back to download page.

____________________
#7 UPDATE 23.01.2011

Hardware V2e:
-added a 100ohm pulldown resistor for +5V line
Now, circuit is more stable
This fixes a problem when some of chips worked in non-HV mode and we can't fix the RSTDISBL fusebit.

Firmware 2.07:
-CRITICAL FIX for AT90s1200, AT90s2313, AT90s2323, AT90s2343, AT90s4414, AT90s4434, AT90s8515, AT90s8535
(different fusebits and lockbits adresses, see datasheet)
-also, improved AT90s2313 default fuses - short start-up time is disabled by default.
-added new chips to uc's database: Atmega406, Atmega16HVB, Atmega32HVB (not listed above). Those are supported theoretically, see datasheet how to program "battery magament avr's". 
-fixed bug in rs232 info
FUSEBITS: internal 1MHz clock, EESAVE enabled ( L:0xE1 H:0xD1 )
Compiled with basc-avr 2.0.4.0

____________________
#8 UPDATE 05.03.2011

Firmware 2.08:
-fixed default fuses values for: Attiny28, Atmega161, Atmega163.
-AT90s2313 still was bugged (after critical fix in 2.07) - FIXED
-now, you can use following (backwards compatible with m8) uC as doctor chip:
 Atmega88, Atmega88P, Atmega168, Atmega168P, Atmega328, Atmega328P.
 Code for 16kB and 32kB chips will send uC names trough uart (like in 2.04 firmw).

FUSEBITS: internal 1MHz clock, EESAVE enabled: 
    M8       L:0xE1 H:0xD1
    M88,M168 L:0x62 H:0xD7 E:0xF9
    M328     L:0x62 H:0xD1 E:0xFF

____________________
#9 UPDATE 13.03.2011

Firmware 2.09:
-added support for new chips: Atmega6490A/P, Atmega645A/PA, Atmega6450A/PA
-fixed issue when not writing the extended fuse in Atmega649A/P
-corrected a bunch of chips names with A/P/PA suffix
 This includes terminal names and chips list names (recalculated, 145 supported chips!)
-code optimalisations, still fits into 8kB - shrinked to 7310B :)

FUSEBITS: internal 1MHz clock, EESAVE enabled: 
    M8       L:0xE1 H:0xD1
    M88,M168 L:0x62 H:0xD7 E:0xF9
    M328     L:0x62 H:0xD1 E:0xFF


Hardware V2g:
-added AVCC connection on main PCB - needed in M168 and M328
-added pullup resistor on doctor's reset pin
 Update PCB if you experience problems

_____________________
#10 UPDATE 20.03.2011

Hardware V.2h:
 -added Rx pin as goldpin as 3rd pin in RS232 connector
 -added pulldown resistor for Rx pin - this is NECESSARY when updating to 2.10!


Firmware 2.10:
-new feature: send your own fuses and locks trough terminal, talk with chips with broken signature.

 If you connect terminal Tx pin to PCB Rx pin - manual mode will be enabled automatically.
 This requires Tx-terminal pin to be HIGH and OUTPUT when idle. It must pull up the 10K pulldown.
 If this condition is not met, doctor will work in normal - automatic mode.

USAGE:

 First, doctor will read signature. And if fail, it will ask to type signature manually.
    Type two last bytes of signature in HEX (4 chars) and hit enter.

 Then, doctor will try to read the chip depending on given signature.
    When succeed, select an option:
    1 - write fusebits - this will perform a fuse write cycle with fuse-values from buffer (default).
    2 - modify fusebits - this will let you to type fuses manually, values in buffer will update.
        Type one byte in HEX (2 chars) and hit enter. Repeat for each byte (if exist).
    3 - set lockbits - type new lock value in HEX (2 chars) and hit enter - do this with caution!
        Remember that unused bits are always 1! E.g. if want to enable LB1 and LB2, type FC (11111100)
    4 - erase the chip - this will just erase the chip and locks, it require "allow erase" jumper for safety.
    5 - end - exit programming and drop voltages, now you can safely remove the chip.

 See "fix_tiny13.png" to see how Attiny13 with broken signature was repaired
 See "mess_tiny13.png" to see how the same chip was broken again
 Do not suggest LEDs when in manual mode - they just blinking randomly :)

FUSEBITS: internal 1MHz clock, EESAVE enabled: 
    M8       L:0xE1 H:0xD1
    M88,M168 L:0x62 H:0xD7 E:0xF9
    M328     L:0x62 H:0xD1 E:0xFF

_____________________
#11 UPDATE 30.04.2011

Firmware 2.11:
-fixed bug when not writing the HIGH fusebyte (concerns all chips!)
"Just" a typo which i made during optimalisations for 2.10 firmware :)

FUSEBITS: internal 1MHz clock, EESAVE enabled: 
    M8       L:0xE1 H:0xD1
    M88,M168 L:0x62 H:0xD7 E:0xF9
    M328     L:0x62 H:0xD1 E:0xFF