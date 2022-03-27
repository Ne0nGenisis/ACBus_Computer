# ACBus Computer
A backplane bus for simple 8-bit, 16-bit, and potentially 32-bit computers. 

This is a project started the evening of the 11th of March, 2022, to create a simple Motorola MC68000 based backplane computer. I don't know if it's going to end up materializing without a source of funding to purchase chips, sockets, capacitors, and have PCBs made or source wire wrap testing boards. The scope of the project has changed to be a general purpose bus for a number of potential target CPUs on "System Card Sets", including the MOS Technologies 6502, the Zilog Z80, the Motorola MC68000/MC68010, and the Motorola MC68020/MC68030. 

## System Architecture

The core of the system is a backplane that accepts cards on a 64-pin slot called "ACBUS" (for Anni's Computer Bus, Anni being me) which grounds the cards and provides voltage from a standard ATX power supply, and a number of common uncommitted pins between slots to facilitate communication across the target CPU's address and data buses. 

Tentatively, two alternative versions of this slot exist. 

### ACBUS Extended (ACB-EX)
A 64+36-pin version for CPUs that have more than 40 bus pins plus signaling, as the MC68000 does, with the specific intention to support 32-bit processors such as the Motorola 68030 and, if they may be sourced and understood well enough to create a system architecture for them, MIPS R3000 series CPUs.

### Computer on Module for ACBUS (COM-ACB)
COM-ACB is intended to allow more common motherboard form factors such as uATX without requiring system cards to be unsupported and wear on the card slots, or to make backplanes with a very small number of slots that would greatly restrict expansion possibilities due to the CPU, RAM, ROM, interface devices, and Audio/Video all being on their own cards. 

## Expectations
The current backplane design is an 8-slot board with Baby AT mounting holes that may also be placed into an ATX case, though it would be far less space efficient. 

Power supplies are currently expected to be on the ATX standard to make availability easier. A potential PSU card that accepts a barrel jack to convert 9V, 12V, or 19V DC into the more commonly used 5V and 3.3V used by the machine's components is also on the list of goals for a more compact system. 

8-bit CPUs are expected to require a unique rom to be paired with them, but RAM and peripheral cards might be cross compatible with proper support from the kernel. They are expected to run BASIC. 

16-bit and 32-Bit CPUs might require their own sets of system cards, especially due to the LDS/UDS lines on the Motorola 68000 making memory addressing less straightforward. The MC68000 based machines are hopefully going to run ucLinux or OS-9/68K, but I'm not much of a software kind of girl so I am not aware of the amount of work that would be needed to port them to other machines. 

The target video chip for various systems is currently unknown, but the audio chip, at least for the 16-bit machines, is likely to be a Yamaha YM2612 and a Texas Instruments SN76489, the same sound chip set found in the Sega Genesis/Master System. 

## Boards
### General Purpose
- Board ID-002: Baby AT 8-slot backplane
- Board ID-005: Power Delivery Card
- Board ID-007: ACBUS Prototyping Perfboard Card

### MC68000 / MC68010 "Durandal" Set
- Board ID-001A: MC68000/MC68010 CPU Card (PGA Socket)
- Board ID-003: MC68000/MC68010 CPU PGA to DIP Adapter PCB
- Board ID-004: MC68000/MC68010 CPU COM-ACB Module
- Board ID-006: 4MB SRAM Card
- Board ID-008: 1MB ROM Card
