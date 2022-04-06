# Card Set 001: "Durandal"
The Durandal board set for the ACBUS computer is built to use a Motorola MC68000 or MC68010 CPU without an MMU. So far, three cards specific to it have been designed. 

## Board ID-001A: CPU Card (PGA)
The CPU Card consists of the Motorola MC68000 or MC68010 CPU in a ceramic PGA package, six 74LS245 octal bus transcievers (three for the 23 address lines, two for the 16 data lines, and one for the four byte selection and read/write control signals), decoupling capacitors, and a crystal oscillator matching the speed of the processor used on the PCB, which in my case will be a 10MHz MC68010. It's a small ACBUS card size, at 3"x6" not including the card edge or the extension for the low-profile to full height PCIE card adapter-style bracket, which it has mounting holes to take advantage of. 

![CPU_Board Render](https://user-images.githubusercontent.com/37624825/160970447-37cf19dd-803e-4fdc-a983-0dea9f4c9e54.jpg)

I'm certain this board will need to be redesigned, especially the clock crystal (probably needs a buffer or something to convert the sine wave into a square wave) but I had a good time designing it so that's fine. 

The edge connector on this card is an output that connects to other cards over the bus with this pinout. 

![Durandal Slot Edge Pinout](https://user-images.githubusercontent.com/37624825/160972645-5c4df9b5-4509-4c35-bbce-919ab6829a51.png)

The pins to the left of the address pins are organized as such due to my own previous misunderstanding about where the data strobe lines UDS and LDS belonged, and one clock pin, which might be added back on if/when the clock crystal is moved to the backplane.

## Board ID-006: RAM Card (4MB)
The RAM card is a fullzise 3.5"x7" card that features eight AS6C4008 SRAM modules at 512 kilobytes each, separated into four 1 megabyte banks. 

![RAMBoard](https://user-images.githubusercontent.com/37624825/160979927-b37c4cea-455a-4a71-ad91-f5b3a2f5e54a.jpg)

The RAM banks are assigned bank numbers 1 through 4, addresses $100000 to $4FFFFF by way of a 74LS154 4-bit decoder, which when fed the most significant four bits of the address space (A20 through A23) allows for up to 16 devices with one megabyte of total address space. When the top four bits read 0001, 0010, 0011, or 0100, a RAM bank is selected. 

![Durandal Memory Map](https://user-images.githubusercontent.com/37624825/160980065-20550521-89f0-4623-964c-e9652c33f365.png)

The two smaller logic ICs are for byte selection. With the way that the memory system is constructed, the data in both RAM and ROM is intended to be "striped" across the two chips in the bank. RAM chip A1 has the lower byte while A2 has the upper byte, and the same is true across all banks of RAM and ROM. The ADS and UDS lines are fed into one input of two AND gates each, by way of a 74LS08, and each of the four AND gates either recieves an inverted R/W signal from a 74LS04 or a non-inverted R/W signal from the CPU card. This creates four signals that are used as write and output enable signals for one or both of the ICs in a bank. 

These three ICs, the 74LS154, 74LS04, and 74LS08, or equivalents to replicate their functions, are to be duplicated across all cards to allow for address decoding. 

## Board ID-011: ROM Card (Configurable Capacity)
The ROM card is fundamentally similar to the RAM card, but it only features a single bank of STT 39SF0x0 EEPROM ICs and is assigned to bank 0, between address $000000 and $0FFFFF. 

![ROMBoardV4](https://user-images.githubusercontent.com/37624825/162069318-8ba482ca-41b9-4304-b1fe-77e404725dd5.jpg)

This mapping is due to the fact that the MC68000 CPU begins searching for instructions at the bottom of its address space and if it does not find them, it will halt. Theoretically this could be solved with a coprocessor that serves only to load instructions to RAM, or a signal generated elsewhere such as on the backplane that forcibly disables the RAM and enables the ROM, but for simplicity's sake, this is how I have chosen to do things. 

It was designed with the intent to be universal across *any* CPU with a 16-bit data bus and a 24-bit address bus by way of configuration jumpers, and configurable with either 256KB, 512KB, or 1MB of storage space for ROM code including the system's kernel and device control software, bootloaders for disk-based operating systems, or included operating systems and programs. The configuration settings are as follows. 

#### For 256K
- Use 39SF010 1 megabit ROM ICs or equivalent

#### For 512K
- Use 39SF020 2 megabit ROM ICs or equivalent

#### For 1M
- Use 39SF040 4 megabit ROM ICs or equivalent

#### For MC68000 or MC68010
- Close Jumper J1 pins B and C
- Close Jumper J2 pins A

#### For other 16D/24A CPUs
- Close Jumper J1 pins A
- Close Jumper J2 pins B
