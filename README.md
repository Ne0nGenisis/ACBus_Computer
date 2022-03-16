# ACBus Computer
A backplane bus for simple 8-bit, 16-bit, and potentially 32-bit computers. 

This is a project started the evening of the 11th of March, 2022, to create a simple Motorola MC68000 based backplane computer. I don't know if it's going to end up materializing without a source of funding to purchase chips, sockets, capacitors, and have PCBs made or source wire wrap testing boards. The scope of the project has changed to be a general purpose bus for a number of potential target CPUs on "System Card Sets", including the MOS Technologies 6502, the Zilog Z80, the Motorola MC68000/MC68010, and the Motorola MC68020/MC68030. 

The core of the system is a backplane that accepts cards on a 64-pin slot called "ACBUS" (for Anni's Computer Bus) which grounds the board and provides voltage from a standard ATX power supply, and a number of common pins between slots to facilitate communication across the target CPU's address and data buses. A 64+36-pin version called "ACB-EX" (Annika's Computer Bus Extended) tentatively exists for CPUs that have bus widths larger than 16 to 24-bits as the MC68000 does, and a version that sockets parallel to the motherboard called "COM-ACB" (Computer On Module for ACBUS) to allow more common motherboard form factors such as uATX without requiring system cards to be unsupported and wear on the card slots, or to make backplanes with a very small number of slots that would greatly restrict expansion possibilities due to the CPU, RAM, ROM, interface devices, and Audio/Video all being on their own cards. 

## Expectations
The current backplane design is an 8-slot board with Baby AT mounting holes that may also be placed into an ATX case, though it would be far less space efficient. 

Power supplies are currently expected to be on the ATX standard to make availability easier. A potential PSU card that accepts a barrel jack to convert 9V, 12V, or 19V DC into the more commonly used 5V and 3.3V used by the machine's components is also on the list of goals for a more compact system. 

8-bit CPUs are expected to require a unique rom to be paired with them, but RAM and peripheral cards might be cross compatible with proper support from the kernel. They are expected to run BASIC. 

16-bit and 32-Bit CPUs might require their own sets of system cards, especially due to the LDS/UDS lines on the Motorola 68000 making memory addressing less straightforward. The MC68000 based machines are hopefully going to run ucLinux or OS-9/68K, but I'm not much of a software kind of girl so I am not aware of the amount of work that would be needed to port them to other machines. 

The target video chip for various systems is currently unknown, but the audio chip, at least for the 16-bit machines, is likely to be a Yamaha YM2612 and a Texas Instruments SN76489, the same sound chip set found in the Sega Genesis/Master System. 
