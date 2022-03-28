# Card Set 001: "Durandal"
The Durandal board set for the ACBUS computer is built to use a Motorola MC68000 or MC68010 CPU without an MMU. So far, three cards specific to it have been designed. 

## Board ID-001A: CPU Card (PGA)
The CPU Card consists of the Motorola MC68000 or MC68010 PCU in a ceramic PGA package, six 74LS245 octal bus transcievers (three for the 23 address lines, two for the 16 data lines, and one for the four byte selection and read/write control signals), decoupling capacitors, and a crystal oscillator matching the speed of the processor used on the PCB, which in my case will be a 10MHz MC68010. 
