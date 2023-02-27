  As of April of 2022, the project was put on pause but my hyperfixation has shifted back to computers and I'm considering picking this project back up. As an aside, I also have a job now (thanks, therapy), so I have the ability to purchase my parts and boards eventually. At the time this project was paused, my focus had shifted away from an AT-style motherboard with PC-style system component cards to something that would be able to be produced on the prototyping rates offered by companies such as PCB Way and JLCPCB, 10x10cm boards on a small multi-socket backplane. An integrated single board design and keyboard interpreter was also tentatively in the works, but it was slow going. Helps me understand why computers take so long to design hardware for. 
  
  Instead of using 64-pin edge connectors, the modern Durandal ACBus prototype design utilizes a 96-pin DIN 41612 connector, also featured on Apple's Processor Direct Slots (PDS) and NUBUS, though the pin arrangement on the board also allows for blocks of 2.54mm/0.1" pitch pin headers to be used. While cheaper, they are also far harder to find. This means that the existing 68010 processor computer design is not at all stressed by the use of exactly as many (functional) pins as the CPU has, and the system's backplane could also be repurposed for both more advanced systems such as the 68020/68030, and less advanced systems such as the 6502 and Z80, without requiring the use of large cards with gigantic card edges. 

  In addition to this backplane model, there is also a condensed single board prototype in an ITX format that contains all of the componentry that the backplane system uses, but uses less decoding logic as each individual module is not required to use its own memory and device decoder circuits. 

# Backplane System

  The ACBus Backplane System uses small 10x10cm PCBs intended to be purchasable at JLCPCB's discounted prototyping rate of just a few dollars for a set of 5 boards up to 4 layers. This allows for true internal ground and power planes that would not be available on PCBWay's restricted 2-layer prototyping boards. 
  
## Backplane Board 

  The backplane PCB contains four 96-pin DIN-41612 connectors alongside a MOLEX Micro-Fit Jr. connector providing 5v and 12v to the slots, and four small holes that can be used to connect the system to standoff feet or a chassis designed to hold it. The prototype will be able to host up to four modules. The intended modules are listed below. 
  
## CPU Module (016A)

  The CPU module A variant integrates a PGA Motorola 68000 or 68010, as well as a number of line drivers (74LS245) to ensure the CPU has control of the bus, and the system's crystal oscillator and clock dividers to derive all of the necessary frequencies for the system components. The CPU's address, data, and memory control bus, as well as the various system clock signals, are exposed to the 96-pin connector at the bottom of the card. 
  
## RAM/ROM Module (RAM - 020, ROM TBD)

  The prototype RAM module features four 512 kilobyte/4 megabit SRAM packages (AS6C4008) and decoder circuitry in the form of a 74LS154 for device decoding, using the last 4 address lines and decoding them into 16 chip enable lines for device selection, and a 74LS04 and 74LS32 to decode the R/W, LDS, and UDS signals from the CPU and using them to create four enable signals for the memory packages. This is necessary as the system uses 8-bit memory packages connected in parallel to the 16 bit memory bus, and selecting only one or the other is done using the following signals: 
  
  - R/W low + UDS low = Read Upper Byte (Output Enable on High Byte RAM and ROM)
  - R/W low + LDS low = Read Lower Byte (Output Enable on Low Byte RAM and ROM)
  - R/W high + UDS low = Write Upper Byte (Write Enable on High Byte RAM)
  - R/W high + LDS low = Write Upper Byte (Write Enable on Low Byte RAM)

  While not currently designed, the ROM card would be nearly identical, aside from not utilizing the Write memory lines and having only two memory packages. 
  
  The ROM is hard coded to device block 0, while the RAM banks are assigned blocks 1 and 2. Extended memory can occupy blocks 3 and 4 for up to 4MB of RAM, and further devices will use blocks 5 through F. 
  
## Serial Communication Module (TBD)

  The Serial Communication module features a 68681 DUART chip, hosting two serial communication channels at block 5, as well as the 74LS154 device decoder. It is connected to the first 8 bits of the data bus and the first 4 bits of the address bus on the CPU, as well as the Data Transfer Acknowledge (DTACK) signal line. 
  
# Integrated Board (027)

  The integrated PCB is in a Mini ITX format and features all components mentioned so far, including the CPU, RAM and ROM, the DUART, memory and device address decoding, and the oscillator/divider circuitry. On top of that, the board also features an ACBus/96 expansion slot for future use with expansion devices. This port exposes the full Data and Address buses, as well as the R/W, AS, UDS and LDS signals, the master clock signal of 15 MHz, and supplies 5 and 12 volts. it will eventually be used for other expansion modules, such as the intended audio and video solutions and keyboard controllers. 
  
  The board is intended to be housed inside a small ITX case and powered by either a Pico ATX power supply, or a 1U Flex ATX power supply. 
  
# Future Modules

  - Video Module, using Yamaha V9938/V9958
  - Sound Module, using Yamaha YM2612/YM3438
  - Keyboard Module, method unknown
  - Storage Module, IDE/CF likely, potentially SD
