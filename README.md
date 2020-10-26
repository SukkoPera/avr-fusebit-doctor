# ATmega Fusebit Doctor (HVPP + HVSP): Fix the fusebits

ATmega Fusebit Doctor is a device for repairing dead ATmega (and ATtiny since v2.04) family AVR microcontrollers by writing correct fusebits. Most common mistakes or problems are a wrong clock source (CKSEL fusebits), disabled SPI programming (SPIEN fuse) or disabled reset pin (RSTDISBL fuse). This simple and cheap circuit will fix you uC in a fraction of a second. If in first case we can help ourself with clock generator, then in 2nd and 3rd cases bring uC back to life is impossible with standard serial programmer. Most of people do not decide to build parallel programmer because its inconvenient and its cheaper and faster to buy new uC.

Originally ATmega Fusebit Doctor was a project by Paweł Kisielewski (Manekinen). One day his website disappeared and the project was at risk of being lost forever. Luckily, I (SukkoPera) managed to salvage it with the help of Wayback Machine and decided to put it on GitHub, trying to preserve all the original contents and history. I hope people will contribute and help make it an even better project.

## High voltage programming
This circuit uses the parallel and serial high-voltage programming method. With those methods, we can talk to our "dead" chips which have reset or isp disabled:
- HVPP = High Voltage Parallel Programming
- HVSP = High Voltage Serial Programming.

## Supported chips
Code to this point supports 145 chips, but not all have been tested. Untested ones are listed *in italic*.

### 1kB
AT90s1200, *ATtiny11*, *ATtiny12*, ATtiny13/A, *ATtiny15*

### 2kB
ATtiny2313/A, *ATtiny24/A*, ATtiny26, *ATtiny261/A*, *ATtiny28*, *AT90s2333*, *ATtiny22*, ATtiny25, AT90s2313, *AT90s2323*, *AT90s2343*

### 4kB
ATmega48/A, *ATmega48P/PA*, ATtiny461/A, *ATtiny43U*, *ATtiny4313*, *ATtiny44/A*, *ATtiny48*, *AT90s4433*, *AT90s4414*, *AT90s4434*, ATtiny45

### 8kB
ATmega8515, ATmega8535, ATmega8/A, ATmega88/A, *ATmega88P/PA*, *AT90pwm1*, *AT90pwm2*, *AT90pwm2B*, *AT90pwm3*, AT90pwm3B, *AT90pwm81*, *AT90usb82*, *ATtiny84*, ATtiny85, *ATtiny861/A*, *ATtiny87*, *ATtiny88*, AT90s8515, *AT90s8535*

### 16kB
ATmega16/A, *ATmega16U2*, *ATmega16U4*, *ATmega16M1*, *ATmega161*, ATmega162, *ATmega163*, *ATmega164A*, *ATmega164P/PA*, *ATmega165A/P/PA*, ATmega168/A, *ATmega168P/PA*, *ATmega169A/PA*, *ATtiny167*, *AT90pwm216*, *AT90pwm316*, *AT90usb162*

### 32kB
ATmega32/A, *ATmega32C1*, *ATmega323/A*, *ATmega32U2*, *ATmega32U4*, *ATmega32U6*, *ATmega32M1*, *ATmega324A*, *ATmega324P*, ATmega324PA, *ATmega325*, *ATmega3250*, *ATmega325A/PA*, *ATmega3250A/PA*, *ATmega328*, ATmega328P, *ATmega329*, *ATmega3290*, *ATmega329A/PA*, *ATmega3290A/PA*, *AT90can32*

### 64kB
*ATmega64/A*, *ATmega64C1*, *ATmega64M1*, *ATmega649*, *ATmega6490*, *ATmega649A/P*, *ATmega6490A/P*, *ATmega640*, ATmega644/A, ATmega644P/PA, *ATmega645*, *ATmega645A/P*, *ATmega6450*, *ATmega6450A/P*, *AT90usb646*, *AT90usb647*, *AT90can64*

### 128kB
*ATmega103*, ATmega128/A, ATmega1280, *ATmega1281*, *ATmega1284*, *ATmega1284P*, *AT90usb1286*, *AT90usb1287*, *AT90can128*

### 256kB
ATmega2560, ATmega2561

## About
Just put your dead mega in socket, press the START button, and enjoy your good-as-new processor. There are three slots on board, for most common AVR’s, pins compatible with: ATmega8, ATmega16, ATtiny2313. There is also an extra goldpin connector with all signals so you can attach adapters:
- "#1 adapter" as HVPP extension, for 20pin ATtiny26 compatible and 40pin ATmega8515 compatible processors.
- "HVSP adapter" for 8pin and 14pin HVSP processors

Or make your own adapters for other types of processors, in trough-hole or surface-mounted, you can use the breadboard for this – just connect signals to correct pins. How? Check your AVR datasheet, go to "memory programming” and then "parallel programming” – check the signal names, all signals are described under the DIP40 slot. In doctor memory there is a lot of free space so project may be developed all the time. One sided PCB with 55mm x 92mm dimensions. On top side you need to solder several jumpers, or, make this PCB as double sided – choose yourself.

Resistors from R7 to R23 may be in 100ohm to 10K, but i suggest from 470ohm to 1K.

ATTENTION! While mounting the DIP40 slot, you must to remove it pins from 29 to 37. These pins must not have electrical contact with inserted uC pins, traces runs there only to make the board smaller (onesided). Take a look at pic on the left, these you must remove from slot.

## Usage
The ALLOW ERASE jumper allows doctor to erase whole flash and eeprom memory, if it is open, doctor will never erase memory but may not cure device if lockbits are enabled, so you choose.

After insert dead uC and press the START button, doctor will initiate the parallel or serial high-voltage programming mode. This is chosen automatically, device will recognize HVSP adapter and start to work in HVSP mode. After that, doctor wait for high state at RDY/BSY line. Then, read device signature and check if it supports it. Next, memory erase is performed if user allows that. Then lockbits are checked, and if they not blocking device, doctor sets all fusebits to fabric, having regard to whether there are extended fusebits or not. Some of older AVR have only one byte of fuses – LOW – and this is also included. After
fusebits are verified, the proper leds is flashed.

### Leds explanation
- Green on – patient successfully cured, fusebits repaired. If lockbits are enabled, just verify fusebits with factory ones – and if they ok – light up green.
- Red on – signature problem, can’t read, no device in socket, or no such signature in database.
- Green flashing – signature ok, fusebits are wrong. Lockbits enabled, chip erase permission required (read below).
- Red flashing – signature ok, no lockbits, but for some reason can’t write new fusebits.

## Terminal
Note that terminal is not needed, device works without pc, and all we want to know we get from leds.

You can find extra RS232 output, and connecting this to the terminal, sends all information about fixing process – see exemplary printscreens in gallery. All the info is sent "on the fly" via uart. Use proper converter to connect this with pc. If you have COM port for RS232, use MAX232 based converter (eg this). If you are using laptop, use a USB converter.

### Terminal settings
- Baudrate: 4800
- Parity: none
- Data bits: 8
- Stop bits: 1
- Handshake: none

## Other
Use one of the following microcontrollers as the doctor-chip: ATmega8, ATmega88, ATmega88P, ATmega168, ATmega168P, ATmega328, ATmega328P – and their newer/low-voltage "A” or "L” versions.

Use stabilized 12V supply voltage. Higher voltage can damage the patient chip!

Code was written based on high-voltage parallel and serial programming section of datasheet of suitable AVRs.

### Fusebits
Internal 1MHz clock, and enabled EESAVE bit – see README file.

If you use a brand new chips as doctor, you don’t need to change anything – 1MHz clock is already set as default. EESAVE bit is optional. It disallows to erase the eeprom when firmware is actualized, eeprom is used to store the fixed chips counter which is sent trough UART.

## Manual Mode
UPDATE 2.1X ADDS NEW FUNCTIONALITY!

Send your own fuses and locks trough terminal, talk with chips with broken signature. If you connect terminal TX pin to PCB RX pin – manual mode will be enabled automatically. This requires TX-terminal pin to be HIGH and OUTPUT when idle. It must pull up the 10K pulldown. If this condition is not met, doctor will work in normal – automatic mode.

### HowTo
First, doctor will read signature. And if fail, it will ask to type signature manually.

Type two last bytes of signature in HEX (4 chars) and hit enter.

Then doctor will try to read the chip depending on given signature.
When this succeeds, select an option:
1. Write fusebits: this will perform a fuse write cycle with fuse-values from buffer (default).
2. Modify fusebits: this will let you to type fuses manually, values in buffer will update. Type one byte in HEX (2 chars) and hit enter. Repeat for each byte (if exist).
3. Set lockbits: type new lock value in HEX (2 chars) and hit enter – do this with caution! Remember that unused bits are always 1! E.g. if want to enable LB1 and LB2, type FC (11111100).
4. Erase the chip: This will just erase the chip and locks, it requires the "allow erase" jumper for safety.
5. End: exit programming and drop voltages, now you can safely remove the chip.

Do not pay attention to the LEDs when in manual mode – they will just blink randomly :).

## License
Manekinen's original licensing terms say:

> Any modifications allowed, do not remove this README! from archive. Do not remove info from pcb and code.
>
> Any usage of this project in commercial/profit purposes is prohibited.

They are a bit vague but they seem to match [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1) pretty well, so I think that can be used whenever a formal license is needed.

Note that the firmware sources are not available. They have never been disclosed as far as I know.

## FAQ – Frequently Asked Questions (and Answers)

Q: No sign of life, no leds are working.
A: Critical bugs on pcb, poorly programmed chip.

Q: Red led is on.
A: Chip si not recognized. Make a voltage measurements. In idle, measure voltages on +12 RESET and +5 SUPPLY at female goldpin connector – you should get 0V or close to 0V on both. After the START button is pressed, you should get close to +12V and 5V for one second. If not, check transistors, if they are ok and if they are soldered ok.

Q: Red led is on.
A: Bugs on pcb, traces are packed densely and its very possible that you have invisible gap, shortcut, or dry joint. Check everything with multimeter, but PRECISELY.

Q: Red led is on.
A: Connect device to the terminal to get repair log. Press start to receive infos.

Q: Received "Init programming...” and nothing more – OR – received signature is "00 01 02” or "FF FF FF”.
A: Chip is broken, or there still are bugs on pcb – look above.

Q: Received signature is "1E 90 00", "1E 1E 1E", or something familiar (meaningful data).
A: Chip is good, it initiates, look for shortcuts on DATA, BS, XA lines.

Q: Green led is on / "Verifying... – OK!" received, but chips don’t work with standard programmer.
A: You can be 100% sure that fuses are fixes, chip have hardware ISP damaged or it have some other damage.

Q: What are "Read Signature... FAIL!" and "Trying T2313 pinout... OK" doing in log?
A: All the 20pin chips need to be treated individually. First, device tries to read chip with standard schematic, and if it fails ("FAIL!”), then it tries to use schematic for 20pin T2313 compatible chips and then chip is read properly. This is normal behavior, this not a bug.

Q: What are `<[2J` trashes doing in log?
A: This is a terminal clear screen sequence, turn on the "VT-100” emulation in terminal settings.

Q: I’m trying to type data into terminal but no chars appearing.
A:Make sure you set handshake to NONE in terminal settings.

Q: After typing data into the terminal, I can’t confirm them with return key and can’t type next ones.
A: When pressing return, your terminal must have to send the CRLF chars, if not, check your settings.

Q: This still doesn’t help me, I tried everything but still have the problem.
A: Ask in comments below :) Post firmware version and pcb version with which you try to work, paste the repair log.

Q: Are all those 1K series resistors (R7 through R23) really needed here?
A: No, you can build the circuit without them. But remember, if for some reason out patient will not enter in the programming mode and continue with its code, then logic state conflict will occur between two microcontrollers which can damage them permanently. These resistors are to protect the circuit against such situations. I strongly recommend to build it exactly as schematic says.

Q: Pull-down resistors for 12V and 5V lines (R24 and R27) are heating up quite strongly in manual mode, and whole circuit takes more power, can i change them for something higher value?
A: Yes, but circuit can work incorrectly with some of the patients. When idle, voltages should be near 0V, and when powering on or off, their edges should have proper
steepness to provide good timing (see entering high voltage programming in datasheet). Because only simple bipolar transistors are used, these resistors guarantee above requirements. The interesting case is an ATtiny2313 problem when all the fuses were correctly burned, without one, the RSTDISBL. As it showed up, because of bad edges of 12V reset voltage, this uC although was working in parallel mode, but not in high voltage, so it was not allowing to change that fuse – this is my own interpretation so i can be wrong.

Q: My chip is read properly but doctor can not write new fuses, allow erase is enabled.
A: If the ISP programmer acts the same way, then your chip is damaged, nothing can do.

Q: Without a patient, circuit acts awkward, it freezes, and goes on when i put my finger near the traces.
A: This circuit is not meant to be used without a patient. It acts in such way because when entering in programming mode, it is waiting for a high state on the RDY pin from patient. This pin is not pulled down and works as high impedance input, so electrostatic charge from your finger is read as high state and code goes on further.

Q: Chip names are not appearing in the log, i see "no names in 8kB ver" instead.
A: Chip names are not displayed in 8kB versions of the firmware, i.e. for ATmega8 and ATmega88 – because names don’t fit in such memory space. If you want the names, use ATmega168 or ATmega328 chip and burn proper firmware. ALWAYS use the newest version of the firmware. Hex and bin files are the flash memory files, use one of them. No need to program eeprom memory.
