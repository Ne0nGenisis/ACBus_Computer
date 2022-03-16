# ACBus Computer
A backplane bus for simple 8-bit, 16-bit, and potentially 32-bit computers. 

This is a project started the evening of the 11th of March, 2022, to create a simple Motorola MC68000 based backplane computer. I don't know if it's going to end up materializing without a source of funding to purchase chips, sockets, capacitors, and have PCBs made or source wire wrap testing boards. The scope of the project has changed to be a general purpose bus for a number of potential target CPUs on "System Card Sets", including the MOS Technologies 6502, the Zilog Z80, the Motorola MC68000/MC68010, and the Motorola MC68020/MC68030. 

## Expectations

8-bit CPUs are expected to require a unique rom to be paired with them

on a 64-pin slot called "ACBUS" (for Anni's Computer Bus) which grounds the board and provides voltage from a standard ATX power supply, and a number of common pins between slots to facilitate communication across the target CPU's address and data buses. A 64+36-pin version called "ACB-EX" (Annika's Computer Bus Extended) tentatively exists for CPUs that have bus widths larger than 16 to 24-bits as the MC68000 does, and a version that sockets parallel to the motherboard called "COM-ACB" (Computer On Module for ACBUS) to allow more common motherboard form factors such as uATX without requiring system cards to be unsupported and wear on the card slots, or to make backplanes with 
