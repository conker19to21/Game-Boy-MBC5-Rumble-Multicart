# Game Boy MBC5 Rumble Multicart

This is a flashable MBC5-based multicart for the Game Boy. You can make a 2-in-1 or 4-in-1 cartridge, that changes games based on a button press or power cycling the Game Boy. With this board you can also make a single game, but with the addition of a pressable reset button on the cartridge.

I had adapted the DC rumble motor to the board to allow the option to have rumble availability. This does NOT make non rumble based games have rumble feedback.

This board allows the option to allow both rumble and non rumble games in 1 cart with full save functionality!

Original files were converted from Eagle to KiCad cleaned and modified to add the changes.

Please note you will require either a Hot Air rework station or Hot Plate heating station to secure the DC motor properly to the board.

The Rumble feature is optional and if you decide not to use it exclude the following:

R11,
R12,
M1,
D1,
Q2


Battery hold down is NOT included however can be aquired at the following 2 links:

<a href="https://oshpark.com/shared_projects/XSjucPvH"> CR2Retainer</a>

<a href="https://www.digikey.com/short/4zrrw5rr"> RETAINER</a>

When installing D1 make sure it is in the correct orientation with diode line inside white boxed outline as seen in photo:

![image](https://github.com/conker19to21/Game-Boy-MBC5-Rumble-Multicart/blob/main/IMG_5354.jpg)

Special Thanks to Bucket Mouse, HDR and Bonzo!

![image](https://github.com/conker19to21/Game-Boy-MBC5-Rumble-Multicart/blob/main/IMG_5336.jpg)
![image](https://github.com/conker19to21/Game-Boy-MBC5-Rumble-Multicart/blob/main/IMG_5338.jpg)

Please see below for the Mouse's original documentation.

The features are as follows:

- Able to make a cartridge with either 2x 2 MB games or 4x 1 MB games
- Optionally adds a pressable button to the cartridge (no shell cutting required)
- The button can be configured to cycle games on the cart, reset the console, or both
- Configurable to have separate save data for each game, or to share the same save data across multiple games
- Fully compatible with the <a href="https://www.gbxcart.com/">GBxCart RW</a> so you can transfer games and save files to and from the board

Some examples of fun cartridges you can make with this board are:
- A single Pokemon game that has a reset button
- Both Pokemon Red and Blue with separate saves
- Both Pokemon Red and Blue with *the same* save (save files are compatible between versions!)
- Both Pokemon Red and Blue with *the same* save that can switch between versions *during gameplay without resetting* (hotswap!)
- A single copy of Powerpuff Girls with two separate save files

All gerbers and source files can be found in this repo, as this project is fully open source. Technical documentation of the board can be found in the Technical folder.

## Important Things Before You Start

1) To use this board, you need to have an original Game Boy game that uses an MBC5 mapper chip. <a href="https://catskull.net/gb-rom-database/">You can find a list of games and their mappers here</a>. Use the search function. Please note the RAM is in bytes, not bits. Since SRAM in this repo is defined in bits, you need to convert by multiplying the number of bytes by 8.
2) You will need to remove the MBC5 from your donor cartridge for use on this board. This will require a hot air rework station or a hot plate. There's a list below of other parts you can re-use from the donor cartridge.
3) When soldering parts on, it's a good idea to put kapton tape or otherwise cover the bottom cartridge edge. You do not want to get solder on the cartridge contacts.
4) I am not responsible for any damage you do to your self or your property. Attempt this project at your own risk.
5) I do not guarantee design compatibility. You may encounter issues with certain games. There is also a chance I have made an error in the design or the BOM - if this is the case, I will do everything I can to address the problem as quickly as possible.
6) If you are using this board to make games other than for personal use, you must have permission from the originator to use and distribute any ROM images or other related material. You are responsible for making sure you adhere to any license requirements.

DO NOT use my circuit boards for profiting from stolen work - this especially includes homebrew content, ROM hacks, and using fan-made labels without permission from the originator. **Support original creators!**

## Board Characteristics and Order Information

The zipped folder contains all the gerber files for this board. The following options **must** be chosen when ordering boards for yourself.

- Thickness: 0.8mm
- Surface Finish: ENIG
- Gold Fingers: Yes, 30° chamfer

You can use the zipped folder at any board fabricator you like.

<a href="https://oshpark.com/shared_projects/OoMrqrWw">The board is also listed on OSH Park as well.</a> **Be sure to get them in 0.8mm thickness if you order from here.**

## Required Equipment

The EEPROMs on the board needs to be programmed somehow. I recommend using the GBxCart, as mentioned. These boards are fully compatible with it, and it makes reflashing games extremely easy using <a href="https://github.com/lesserkuma/FlashGBX">lesserkuma's FlashGBX software</a>.

Alternatively, you can buy an EEPROM programmer with a TSOP adapter. The downside to this method is that you have to desolder the chip every time you want to program it. The <a href="https://flashcatusb.com/">FlashcatUSB</a> is one popular option in retro spaces.

## Battery Safety

When assembling a board, I recommend populating all the parts *except* the battery, and getting it to run initially without it. This is to make it easier to fix any solder connections that might need fixing, without having to worry about getting the battery hot. And if you need to rework anything near the battery after you've put it on the board, be safe and remove it before putting a hot soldering iron next to it.

And this should go without saying, but if you're assembling these boards with a hot plate or hot air, *do not* solder the battery on this way. You should use an iron, and keep heat off of the battery as much as possible. 

(Also check polarity!)

## Board Configurations

There's a lot to cover here. There are four separate switches to configure, and two different sizes of SRAM to pick from.

*Note that you can simply solder bridges from the middle pads of the switches to the left or right to the "ON" or "OFF" positions, instead of installing an actual switch.*

### SRAM Size Selection

There are two sizes of SRAM you can use, and the type you use will dictate how your save data is stored on the cartridge and if it's shared between games or not.

- If you use a 1 Mbit SRAM (like the AS6C1008), then each game you put on the cartridge will have its own separate save files. If you program multiple copies of the same game, then you can effectively have multiple save files on the same cart. Easy example is Pokemon games - they only let you have one save file, but if you put Pokemon Red on the multicart four times, then that gives you four separate save files!
- If you use a 256 Kbit SRAM (like the AS6C62256) then all the games you put on the cartridge will *share* the same RAM space.  This feature is probably only useful for Pokemon games. As an example: this means that if you made a cart that has Pokemon Red and Blue on it, you would play both versions with the same save data, as save data between the two games are compatible with each other.

### Game Cycling Mode Switch (SW2)

SW2, split into two separate switches SW2A (top half) and SW2B (bottom half), controls how you change games on the cartridge. The following table describes the different settings:

| Mode | SW2A (Bottom) | SW2B (Top) | Game change with reset? | Game change with button press? | Does the button reset? |
| ---- | ---------- | ------------- | ----------------------- | ------------------------------ | ---------------------- |
| 1    | OFF        | OFF           | No                      | Yes                            | Yes                    |
| 2    | OFF        | ON            | No                      | Yes                            | No                     |
| 3    | ON         | OFF           | Yes                     | Yes                            | Yes                    |
| 4    | ON         | ON            | Yes                     | No                             | No                     |

*Note: Mode 4 does not give function to the push button at all.*

The "game change" method in this table describes how you advance down the "game" columns described in the table for SW3.

### Game and Save Data Configuration Switch (SW3)

SW3, split into two separate switches SW3A (bottom half) and SW3B (top half), controls the order in which the ROM banks (the games) and the RAM banks (the save data) cycle. This table assumes you are using a 1 Mbit SRAM chip. If you are using a 256 Kbit SRAM, then every entry in the "RAM Banks" column can be described as "1x 256 Kbit", and all the "Game" columns will share that single RAM bank.

Please note that SW3A and SW3B are *different* than the SW3A and SW3B on the MBC3 Multicart PCB.

| Mode | SW3A (Top) | SW3B (Bottom) | ROM Banks  | RAM Banks   | Game 1     | Game 2     | Game 3     | Game 4     |
| ---- | ---- | ---- | ---------- | ----------- | ---------- | ---------- | ---------- | ---------- |
| A    | ON   | OFF  | 2x 2 MB    | 4x 256 Kbit | ROM1, RAM1 | ROM1, RAM2 | ROM2, RAM3 | ROM2, RAM4 |
| B    | OFF  | OFF  | 4x 1 MB    | 4x 256 Kbit | ROM1, RAM1 | ROM2, RAM2 | ROM3, RAM3 | ROM4, RAM4 |
| C    | ON   | ON   | 2x 2 MB    | 2x 256 Kbit | ROM1, RAM1 | ROM2, RAM2 |            |            |
| D    | OFF  | ON   | 2x 1 MB    | 2x 256 Kbit | ROM1, RAM1 | ROM2, RAM2 |            |            |

*Note: Mode D is useless. Just use Mode C instead.*

### Game Mode Examples

Here's a list of example cartridges you can make with these settings:
1) Pokemon Red, Blue, Yellow, and Green on one cartridge with separate save files that changes only via pressing the button, which also resets the game: **Mode 1B** with 1 Mbit SRAM
2) Pokemon Red and Blue with separate save files that changes by pressing the button *or* cycling power on the Game Boy: **Mode 3C** with 1 Mbit SRAM
3) Pokemon Red and Blue with the same save file that hotswaps when you press the button on the cartridge (changing games during gameplay): **Mode 2C** with 256 Kbit SRAM

## How to Program Games

When using the GBxCart to program multiple games to the cartridge, it's recommended to turn SW2A and SW2B to the OFF position. To change ROM/RAM banks to program, simply press the SW1 tactile button between programming steps. Using FlashGBX's "Refresh" button should show that the game information on the left of the screen changes after pressing the button.

If you're programming the flash chip separate from the board, you'll need to concatenate all the ROM files together into one large 4 MB file to program the chip with.

## Test Points and Final Checkout

On the back of the board are five test points. Here's where they are connected:

- TP1: SRAM supply voltage
- TP2: Battery voltage (after R1)
- TP3: Battery voltage (positive terminal of battery)
- TP4: Ground
- TP5: VCC input voltage

After you assemble your game, you should measure the current out of the battery. But first, you should program it with the GBxCart, or if you programmed the EEPROM separately, put it into a Game Boy and cycle power once. Then, flip the PCB upside down on a non-conductive surface (not your leg), and set your multimeter in DC millivolts (or volts). Put the positive probe on TP3 and the negative probe on TP2. If you used a 10kΩ for R1, as indicated in the BOM, you should read a voltage in the single or tens of millivolts. If you have something much higher, especially voltages above 100mV, then you likely have an issue or short circuit on the board somewhere.

**Note: You need to power up the game at least once before battery currents will make sense - the battery management ICs can start up in an unknown state before applying main power to the board.**

To estimate battery life, see <a href="https://github.com/MouseBiteLabs/Game-Boy-MBC5-Cartridge/tree/main/Technical#estimating-battery-life">this section in the MBC5 Technical Design Document</a>, or for more in-depth analysis, <a href="https://hackaday.io/project/11864-tritiled/log/72554-determining-maximum-runtime-176-to-202-years-cr2032">this Hackaday post</a>.

### Battery Size Considerations

The coin cells commonly used on Game Boy carts in order of increasing size are CR2016, CR2025, and CR2032. The CR2032 is the thickest, but yields the longest battery life.

Batteries that are as large as CR2032 will fit inside the shell, *however*, due to the thickness of the CR2032, using one makes it so the shell cannot be pressed down very easily. This makes the button inside the shell difficult to press reliably. For this reason, I recommend using a CR2025 in builds. The battery life should easily last more than 10 years. But if you want to use a CR2032, you should only expect to make a cart that changes games via power cycling only.

<a href="https://github.com/MouseBiteLabs/Game-Boy-MBC5-Cartridge/tree/main/Technical#estimating-battery-life">See this section in my main MBC5 repository for estimating battery life here.</a>

I haven't tested it, but I believe using battery holders instead of pre-tabbed batteries will similarly cause issues with trying to press the button in the middle of the cartridge.

### Why not FRAM?

This board is only suitable for using SRAM. One downside to SRAM, if you haven't figured it out yet, is that you need a battery to keep the SRAM powered on even when the game is turned off. So eventually the battery will die, and your save data is lost. Some people have used FRAM, or Ferroelectric RAM, to keep save data around even after the battery dies (specifically, the popular part that's used for FRAM carts is the FM18W08). But, using this FRAM chip has a handful of downsides, and the benefit of keeping save data after the battery dies *in my opinion* does not outweigh the cons, which are as follows:

1) Quality, new stock, 5V tolerant FRAM is expensive ($12+ per part).
2) Cheaper FRAM chips from eBay or Aliexpress are notoriously flaky (anecdotally, ~50% success rate).
3) FM18W08 maxes out at 256K (which is restrictive for multicarts).
4) FRAM memory access requires different chip select timing than SRAM, and the Game Boy expects SRAM, so it is not natively compatible with FRAM carts. The Gameboy Color specifically cannot (easily) be made to properly access FM18W08 chip. You *can* use an OR gate and add the CLK on the cart edge to try to achieve the necessary timing, but it only works (properly) for DMG/MGB/SGB, not the GBC. It usually *works* in practice for GBC, but it's technically a datasheet violation and can potentially cause issues in edge cases. <a href="https://github.com/Gekkio">(Thanks to gekkio for pointing this out!)</a>

Brand new SRAM chips are ~$3, and having the SRAM footprint also allows you to use SRAM from an original cart if desired. You will *easily* get more than a decade of life running on a battery. You're already assembling this cartridge; you can dump the save and replace the battery before then!

Note that this isn't to throw shade at any FRAM-based carts, but for me personally, it's more trouble than it's worth.

## Board Fitment

The shape of this board was originally meant to mimic original Game Boy circuit boards as closely as possible (v1.1 and earlier). Unfortunately, when placed in some aftermarket Game Boy cartridge shells (like those from Cloud Game Store), the circuit board has a lot of freedom to rotate around the main screw hole in the bottom-middle of the cartridge. This can cause misalignment when you put it in a Game Boy, which can cause a game to either not load properly (garbled Game Boy logo) or shut off the Game Boy because of a short circuit. This isn't *dangerous* or anything, just annoying.

In order to make the boards fit nicer in any kind of shell, for v1.4 I added extended tabs of circuit board material to the edges of the cartridges to keep it from rotating too much in shells, which was suggested to me by <a href="https://github.com/orangeglo">orangeglo</a>! (Thanks!)

If you're having trouble fitting the circuit board into a shell, because the tabs interfere with the cart edges, you can safely sand or trim them down as there is no copper within the tabs themselves. The only shell that appears to require any kind of trimming are Kitsch-Bent shells.

## Bill of Materials (BOM)

*Please note that there was an error in the published BOM before February 24, 2024. If you assembled your board before that date, I recommend you replace R5, R6, and C8 to their new values listed below.*

| Reference Designators | Value/Part Number      | Package        | Description        | Source                                           |
| --------------------- | ---------------------- | -------------- | ------------------ | ------------------------------------------------ |
| B1                    | CR2025, CR2016, CR2032*| See note above | Backup Battery     | [https://mou.sr/3PLccol](https://mou.sr/3PLccol) |
| C1                    | 0.1uF                  | 0603           | Capacitor (MLCC)   | [https://mou.sr/3ENc15O](https://mou.sr/3ENc15O) |
| C4                    | 0.1uF                  | 0603           | Capacitor (MLCC)   | [https://mou.sr/3ENc15O](https://mou.sr/3ENc15O) |
| C5                    | 0.1uF                  | 0603           | Capacitor (MLCC)   | [https://mou.sr/3ENc15O](https://mou.sr/3ENc15O) |
| C6                    | 10uF                   | 0603           | Capacitor (MLCC)   | [https://mou.sr/3mZtSkF](https://mou.sr/3mZtSkF) |
| C7                    | 0.1uF                  | 0603           | Capacitor (MLCC)   | [https://mou.sr/3ENc15O](https://mou.sr/3ENc15O) |
| C8                    | 0.01uF                 | 0603           | Capacitor (MLCC)   | [https://mou.sr/3AsRwK1](https://mou.sr/3AsRwK1) |
| C12                   | 0.1uF                  | 0603           | Capacitor (MLCC)   | [https://mou.sr/3ENc15O](https://mou.sr/3ENc15O) |
| Q1                    | 2N7002                 | SOT-23         | N-Channel FET      | [https://mou.sr/3rgfh6J](https://mou.sr/3rgfh6J) |
| Q2                    | SN74AHC1G126           | SC70           | NPN FET            | [https://mou.sr/3YlwRnW](https://mou.sr/3YlwRnW) OR <a href="https://www.aliexpress.com/item/1005005140909500.html?spm=a2g0o.order_list.order_list_main.5.637818020QcNX1"> AliExpress</a>|
| R1                    | 10k                    | 0603           | Resistor           | [https://mou.sr/3riR7IH](https://mou.sr/3riR7IH) |
| R5                    | 130k                   | 0603           | Resistor           | [https://mou.sr/3MjXliy](https://mou.sr/3MjXliy) |
| R6                    | 130k                   | 0603           | Resistor           | [https://mou.sr/3MjXliy](https://mou.sr/3MjXliy) |
| R8                    | 10k                    | 0603           | Resistor           | [https://mou.sr/3riR7IH](https://mou.sr/3riR7IH) |
| R9                    | 130k                   | 0603           | Resistor           | [https://mou.sr/3MjXliy](https://mou.sr/3MjXliy) |
| R10                   | 49.9k                  | 0603           | Resistor           | [https://mou.sr/3Q3NRZO](https://mou.sr/3Q3NRZO) |
| R11                   | 15Ω                    | 0603           | Resistor           | [https://mou.sr/3zYvyRE](https://mou.sr/3zYvyRE) OR <a href="https://www.aliexpress.us/item/2251832678021377.html?spm=a2g0o.order_list.order_list_main.68.31621802J8yZUJ&gatewayAdapt=glo2usa4itemAdapt"> AliExpress</a>|
| R12                   | 30k                    | 0603           | Resistor           | [https://mou.sr/46kfpCa](https://mou.sr/46kfpCa) OR <a href="https://www.aliexpress.us/item/2251832678021377.html?spm=a2g0o.order_list.order_list_main.68.31621802J8yZUJ&gatewayAdapt=glo2usa4itemAdapt"> AliExpress</a>||
| SW1                   | See note               | 5.2 x 5.2mm    | Tactile Switch     | [https://mou.sr/3uipCQz](https://mou.sr/3uipCQz) OR see note |
| SW2                   | CAS-D20TA              | J Form Lead    | Dual SPDT          | [https://mou.sr/46gGqF1](https://mou.sr/46gGqF1) |
| SW3                   | CAS-D20TA              | J Form Lead    | Dual SPDT          | [https://mou.sr/46gGqF1](https://mou.sr/46gGqF1) |
| U1                    | 29F032, 29F033         | TSOP-40        | Flash EEPROM       | AliExpress or eBay                               |
| U2                    | MBC5                   | QFP-32         | MBC5 Mapper        | Donor MBC5 Game Boy cartridge                    |
| U3                    | AS6C62256, AS6C1008    | SOP-28, SOP-32 | SRAM               | [https://mou.sr/3sFegFF](https://mou.sr/3sFegFF) |
| U4                    | TPS3613                | MSOP-10        | Battery Management | [https://mou.sr/45Ir2kh](https://mou.sr/45Ir2kh) |
| U5                    | SN74HCS74              | TSSOP-14       | Dual Flip Flop     | [https://mou.sr/3QYGEuT](https://mou.sr/3QYGEuT) |
| U6                    | SN74AHC1G126           | SC70           | Tri-State Buffer   | [https://mou.sr/3T9Zdim](https://mou.sr/3T9Zdim) |
| U7                    | SN74AHC1G126           | SC70           | Tri-State Buffer   | [https://mou.sr/3T9Zdim](https://mou.sr/3T9Zdim) |
| U8                    | SN74AHC1G126           | SC70           | Tri-State Buffer   | [https://mou.sr/3T9Zdim](https://mou.sr/3T9Zdim) |
| M1                    | Vibration Motor        | Z43            | DC Motor           | <a href="https://www.aliexpress.com/item/32787320737.html"> AliExpress</a>|
| D1                    |BC817-40                | SOD-123        | Schottky diode     | [https://mou.sr/3LEXYCJ](https://mou.sr/3LEXYCJ) OR <a href="https://www.aliexpress.com/item/1005003618692669.html?spm=a2g0o.order_list.order_list_main.5.31621802J8yZUJ"> AliExpress</a>|

### Note about SW1

SW1 can be either short or long. If the button is long enough, it will sit inside the shell in a way that lets you press it by lightly pressing on the cartridge shell. This way, you can activate it without removing it from the console. This is helpful if you want to change games via a button press.

- If you want to make the button pressable when the cartridge is fully assembled, you need to find a switch that has an extended stem on AliExpress, eBay, or Amazon (**if you find a compatible switch on Mouser or Digikey, please let me know**). The measurements will be 5.2 mm x 5.2 mm, with a height of 3.5 mm. Sometimes these parts are listed as "4 mm x 4 mm" or "5 mm x 5 mm" instead. Check the datasheet, if available, to see if it'll fit the footprint. They should have listing pictures similar to the ones seen here:

![image](https://github.com/MouseBiteLabs/Game-Boy-MBC3-Multicart/assets/97127539/57f93dff-8af2-446d-9d30-69dc870ae9df)

- If you don't care about pressing the button while it's in the shell, like if you are making a multicart that changes games by cycling the power where you wouldn't need it, then you can simply use the TS18-5-25-SL-260-SMT-TR (https://mou.sr/3uipCQz).

### Note about SW2, SW3

Instead of using the somewhat pricey switch designated for SW2 and SW3, you can instead just bridge the pads with solder from the middle pad to the pad in the direction you want to set the switch to. For example - in the below picture, SW3A and SW3B are both in the "ON" position in both cases. (Note that the white switches on the right image are switched to the right.)

![image](https://github.com/MouseBiteLabs/Game-Boy-MBC5-Multicart/assets/97127539/40d1f523-6df1-4596-8ef3-968f2b9fd656)

### REMINDER: SW2A MUST BE IN THE OFF POSITION.

### Usable Donor Cartridge Parts

You can use a few parts from the donor cart on the new board to save some money. Note that you will generally get better reliability with new parts as opposed to old ones. For example: I have seen failed RAM chips from donors in the past.

1) **U2: MBC5** - This one is required
2) **U3: SRAM** - You can use this part *only if* the sum of the RAM space for the games you're using is the same or less amount of RAM that the donor cartridge has. If you plan to have separate save data for every game, you'll probably need to buy an AS6C1008.

You could probably transfer over most of the 0.1uF capacitors but they're pretty cheap anyway, so I generally just recommend buying new resistors and capacitors.

## Things to Remember

- The 29F032 and 29F033 have been known to occasionally be defective upon arrival. They're either used, or new old stock, and usually only available from AliExpress.
- The footprint for the battery can fit a CR2032, CR2025, or CR2016 with solder tabs. The only difference is the mAh capacity (larger number = longer life). If you get Panasonic tabbed batteries, you may have to trim the battery tabs to make them fit on the footprint.
  - For untabbed coin cells, you can find battery retainer adapters online, <a href="https://retrogamerepairshop.com/products/hdr-game-boy-game-battery-retainer?variant=40511013290156">like this one.</a> However, similar to using a CR2032, this will probably prevent easy pressing of the button in the middle of the cart, if added.
- Generally, ROM sizes are conveyed in terms of kilobytes and megabytes (KB, MB). RAM size is usually conveyed in terms of kilobits or megabits (Kbit, Mbit). You can convert Kbit and Mbit to KB and MB by dividing Kbit or Mbit by 8. For example, 256 Kbit = 32 KB.

## Labels

If you want a Bucket Mouse branded label for your cartridge, look no further than <a href="https://krizdingus.com/mousebitelabs/">krizdingus's designs</a>. Special thanks to Kris for designing these, they look awesome! (If you are going to order/print these, use the high-res images hosted on his website, and *keep the labels for personal or non-commercial use only.*)

![image](https://github.com/MouseBiteLabs/Game-Boy-MBC5-Multicart/assets/97127539/3a4cd3d5-f683-40e3-acfb-1b8c549bb1bb)

### Why does SW2A need to be OFF?

SW2A in the ON position previously allowed the multicart to swap games whenever you power cycled the Game Boy. This was achieved by connecting the /RST line on the Game Boy to the CLK input on the flip-flop. The /RST line was held low when power was off by the RESET output of the TPS3613 battery management IC driving the gate of a FET.

The datasheet says this output is a push-pull output, and implies it will behave normally when power is off and the battery is being relied on for power. However, that is not the behavior I have later found to be true. Instead, if the voltage on the VDD pin is too low (like when the power is turned off), this RESET output floats. This causes the FET to not be asserted, and then allows the /RST line to float.

In Modes 3 or 4, where SW2A is in the ON position, /RST is connected to the flip-flop's CLK input. If /RST floats, then CLK floats, which can cause excess current draw from the flip-flop, draining the battery much faster than expected. Therefore, it is recommended to ONLY use a button to change games, and not to rely on power cycling.

A new board to replace this design with something more suitable will be completed in the future. In the meantime, do not put SW2A in the OFF position.

## Resources and Acknowledgements

- <a href="http://www.devrs.com/gb/files/hardware.html">Jeff Frohwein's GameBoy Tech Page</a>
- <a href="https://gbhwdb.gekkio.fi/">Game Boy Hardware Database</a>
- <a href="https://catskull.net/gb-rom-database/">Nintendo Gameboy Game List</a>
- <a href="https://www.gbxcart.com/">insideGadgets discord server for GBxCart RW compatibility requirements</a>
- <a href="https://github.com/lesserkuma/FlashGBX">Lesserkuma's FlashGBX software</a>
- <a href="https://www.alldatasheet.com/datasheet-pdf/pdf/99104/MITSUBISHI/MM1026.html">System Reset IC Datasheet</a>
- <a href="https://www.ti.com/lit/ds/symlink/tps3613-01.pdf?HQS=dis-mous-null-mousermode-dsf-pf-null-wwe&ts=1698238885366&ref_url=https%253A%252F%252Feu.mouser.com%252F">TPS3613 Datasheet</a>
- Board outline modified from <a href="https://tinkerer.us/projects/homebrew-gameboy-cartridge.html">Dillon Nichols's Homebrew Gameboy Cartridge project</a>
- Thanks to <a href="https://github.com/orangeglo">orangeglo</a> for his suggestion of adding spacers around the board edge for better fitment in aftermarket cartridges
- Some components from <a href="https://github.com/adafruit/Adafruit-Eagle-Library">Adafruit's Eagle parts library</a>
- Some components from <a href="https://www.snapeda.com/">SnapMagic</a>
- Thank you to <a href="https://github.com/Gekkio">gekkio</a> for their deep Game Boy knowledge resources, and for collaboration in demystifying some of the design choices on Game Boy cartridges
- Thanks to the awesome members of the <a href="https://moddedgameboy.club/">Modded Gameboy Club</a> for their feedback and support during the entire project development

## License

<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/80x15.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>. You are able to copy and redistribute the material in any medium or format, as well as remix, transform, or build upon the material for any purpose (even commercial) - but you **must** give appropriate credit, provide a link to the license, and indicate if any changes were made.

©MouseBiteLabs 2023
