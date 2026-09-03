# SAP-1_Computer_Analysis
The SAP-1 computer is introduced as a teaching project by Albert Paul Malvino and Jerald A. Brown in their book “Digital Computer Electronics”.

The description of its architecture and operation is presented in the book starting on Page 140 and the diagram starting on page 154. The Parts List is presented on page 501.

The main characteristics of the SAP-1 Computer are: \
- The data stored in registers and processed are 8 bits;
- The Address Bus is 4 bits so a maximum of 16 memory locations can be accessed;
- It does not have a Stack implemented;
- It does not have an Input Device;
- We only have a single output in the form of a Binary Display;
- Interrupts are not implemented;
- Only 5 instructions LDA, ADD, SUB, OUT, HLT;
- The memory is of the ROM type.

## Block Diagram Analysis
The first stage of any project is drawing the Block Diagram, which allows you to visualize the overall picture of the designed system, where you can see the component blocks and the connections between them.

### Original Block Diagram
The original Block Diagram of the SAP-1 Computer can be found in the book "Digital Computer Electronics" by Albert Paul Malvino and Jerald A. Brown, on page 141 and is labeled Figure 10-1.

In the following figure, I present a reproduction of the original Block Diagram of the SAP-1 Computer:

![ Figure 1-1 ](https://github.com/LincaMarius/ISAP-1_Computer_Proiect/blob/main/SAP-1_Computer_Analysis/Pictures1/Figure1-1.png)

### More detailed Block Diagram
I studied the original schematic of the SAP-1 Computer and recreated the block diagram to represent the actual functional blocks as closely as possible and I present it in the following figure:

![ Figure 2 ](https://github.com/LincaMarius/ISAP-1_Computer_Proiect/blob/main/SAP-1_Computer_Analysis/Pictures/Figure2.png)

The HLT control signal was omitted in the original Block Diagram.

The programming mode of the SAP-1 Computer described by the authors is as follows: \
a.	Move selector S2 to the PROG position to enter Programming Mode, \
b.	Select with the S1 switches the memory address whose content you want to modify, \
c.	Select with the S3 switches the Data that you want to be written to the memory at the previously set address, \
d.	Press button S4 to write the new value to memory, \
e.	Repeat steps b, c and d until all necessary changes have been made, \
f.	Move selector S2 to the RUN position, to run the program.

In practice, the content of the RAM memory is edited, after which its content is only read by the SAP-1 Computer.

This Computer has no instruction to write data to memory. This is specific to read-only ROMs. So, one ROM can be used for each program.

### Identification of Computer Components
As we learned in school, a computer can be represented by 3 distinct functional blocks:
- CPU (Central Processing Unit),
- Memory,
- I/O (Inputs / Outputs).

They are interconnected through 3 buses that form the System Bus:
- Data Bus,
- Address Bus,
- Control Bus.

This fact is also presented by the authors in the Book in a simplified form on page 213 in figure 13-1.

A diagram representing a computing system consisting of functional blocks CPU, RAM, I/O and buses is presented in the following figure:

![ Figure 3 ](https://github.com/LincaMarius/ISAP-1_Computer_Proiect/blob/main/SAP-1_Computer_Analysis/Pictures/Figure3.png)

If we check the diagram of the SAP-1 computer we notice that these functional blocks are not grouped, we also cannot identify the three buses on the diagram. We are presented with only the data bus labeled "W Bus".

So, I propose to redraw the Block Diagram of the SAP-1 computer so that we can easily separate these elements: CPU, RAM and I/O, as well as we can easily identify the three buses. 

We get the following Block Diagram:

![ Figure 4 ](https://github.com/LincaMarius/ISAP-1_Computer_Proiect/blob/main/SAP-1_Computer_Analysis/Pictures/Figure4.png)

### Control Unit structure
The SAP-1 computer has a Control Unit made using logic gates.

The Control Unit is built from three blocks:
- Instruction Decoder,
- Step Counter,
- Control Matrix.

The instruction decoder has the structure of a classic decoder and activates a single output depending on the instruction code presented at the input. The number of active outputs is equal to the number of instructions present in the Instruction Set.

The SAP-1 computer is based on micro-step control. For this purpose, a Step Counter block is required. The authors of the SAP-1 computer used a Ring Counter to implement the Step Counter.

The Control Matrix has the role of generating control signals depending on the instruction that is executed in accordance with the current micro-step.

![ Figure 5 ](https://github.com/LincaMarius/ISAP-1_Computer_Proiect/blob/main/SAP-1_Computer_Analysis/Pictures/Figure5.png)

### Binary Display
The simplest output device that can be connected to this Computer is a Binary Display. This device is used in the original construction of the SAP-1 Computer, where it is integrated directly into the structure of this Computer.

My version of the Block Diagram is identical to the original, except that I treated the original Output Register as a standalone block that is connected to the system buses as an Input/Output Device.

The output device consists of a register where 8 bits are written when the I/O control signal is activated and the rising edge of the clock occurs. Each bit from the output of this register is connected to an LED. This is a Binary Display.

![ Figure 6 ](https://github.com/LincaMarius/ISAP-1_Computer_Proiect/blob/main/SAP-1_Computer_Analysis/Pictures/Figure6.png)

### Memory Subsystem
The following figure shows the Memory Block of the SAP-1 computer:

![ Figure 7 ](https://github.com/LincaMarius/ISAP-1_Computer_Proiect/blob/main/SAP-1_Computer_Analysis/Pictures/Figure7.png)

The Memory has two operating modes, dictated by the position of switch S2.

When S2 is in the Run position, the /PGM signal is low and causes the Address Multiplexer to select the address from the input connected to the Memory Address Register. Also, the /CE control signal is connected to the /CE control pin of the RAM. The SAP-1 computer in this mode executes the program from memory.

The Diagram of the Memory Block in Run Mode is as follows:

![ Figure 8 ](https://github.com/LincaMarius/ISAP-1_Computer_Proiect/blob/main/SAP-1_Computer_Analysis/Pictures/Figure8.png)

From this Diagram the Multiplexer can be ignored and we can obtain a simpler and easier to understand Diagram:

![ Figure 9 ](https://github.com/LincaMarius/ISAP-1_Computer_Proiect/blob/main/SAP-1_Computer_Analysis/Pictures/Figure9.png)

Thus, the Memory of the SAP-1 Computer in Run Mode is used as a ROM memory. Control input /CE if high disables the output which is three-state, and if low at the output, the data from the address selected by the Memory Address Register is presented on the Bus.

In this case, the /CE control signal has the #CE function for chip activation but also the #OE (Output Enable) function specific to ROM memories.

When switch S2 is in the “Program” Position, the /PGM signal is high and causes the Address Multiplexer to select the address from the input connected to Address Select Switches S1.

The control input /CE is set low, so at the Memory output, the Data from the Address selected by the Address Select Switches S1 are presented on the Bus.

If the S4 (Deposit) switch is pressed, the /W control signal is set to the low value, which causes the Data present at the input pins whose values are set by the switches marked S3 (Data Select Switches) to be written to the Selected Address.

The Block Diagram of the Memory Block in Programming Mode is as follows:

![ Figure 10 ](https://github.com/LincaMarius/ISAP-1_Computer_Proiect/blob/main/SAP-1_Computer_Analysis/Pictures/Figure10.png)

From this Diagram the Multiplexer can be ignored and we can obtain a simpler and easier to understand Diagram.

![ Figure 11 ](https://github.com/LincaMarius/ISAP-1_Computer_Proiect/blob/main/SAP-1_Computer_Analysis/Pictures/Figure11.png)

Since no Data is read from the Bus, so no Data is transferred to the Bus, this can also be ignored.

![ Figure 12 ](https://github.com/LincaMarius/ISAP-1_Computer_Proiect/blob/main/SAP-1_Computer_Analysis/Pictures/Figure12.png)

We can conclude that in programming mode the Memory is functionally separate from the SAP-1 computer.

So, functionally speaking, the Memory is simply a ROM for the SAP-1 computer.

We can synthesize a Block Diagram for the Memory Subsystem of the SAP-1 and ISAP-1 computers:

![ Figure 13 ](https://github.com/LincaMarius/ISAP-1_Computer_Proiect/blob/main/SAP-1_Computer_Analysis/Pictures/Figure13.png)

We can see an increased complexity of the Memory Subsystem imposed by the need to modify the contents of the Memory using the Control Panel switches.

From what has been presented so far, we have seen that memory is functionally accessed during the execution of a program like a ROM memory, as we can see in the following figure:

![ Figure 14 ](https://github.com/LincaMarius/ISAP-1_Computer_Proiect/blob/main/SAP-1_Computer_Analysis/Pictures/Figure14.png)

### Reset Circuit
The Reset circuit has the role of bringing the computer back to its initial state. Internally, the Central Processing Unit initializes the functional blocks so that they can begin stable execution of any program.

The block diagram of the reset circuit is shown in the following figure:

![ Figure 15 ](https://github.com/LincaMarius/ISAP-1_Computer_Proiect/blob/main/SAP-1_Computer_Analysis/Pictures/Figure15.png)

The circuit consists of a switch marked S5 with two positions followed by a debouncing circuit consisting of an RS flip-flop in the case of the SAP-1 computer.

### Clock Signal Generator circuit
The clock signal is responsible for ensuring synchronous operation of the computer, so that any action takes place at a precise moment in time. Through synchronization, data transfer in the system occurs in a controlled manner.

The SAP-1 computer has two operating modes: \
- Manual – in this mode the clock signal is generated by pressing a button and the program execution advances step by step,
- Automatic – in this mode the clock signal is generated continuously and the program execution is continuous.

For the Automatic mode, the clock signal is generated by an oscillator made with an astable. Its output reaches a T-type flip-flop. The T-type flip-flop divides the input frequency by 2 but we also obtain a signal duty cycle of 50%.

To generate the clock signal in step-by-step mode, we have a two-position switch marked S6 in the diagram followed by an RS-type flip-flop which acts as a debouncing circuit.

The switch marked S7 in the schematic is used to select the operating mode. This is followed by an RS type flip-flop which acts as a debouncing circuit.

Depending on the chosen operating mode, one of the two clock signals is selected using a multiplexer.

The output of the multiplexer is taken by the buffer. Its role is to ensure the necessary fanout because the clock signal reaches all the functional blocks of the computer.

![ Figure 16 ](https://github.com/LincaMarius/ISAP-1_Computer_Proiect/blob/main/SAP-1_Computer_Analysis/Pictures/Figure16.png)

The HLT input inhibits the clock signal when the computer has executed the HALT instruction.

### SAP-1 Computer architecture
The architecture of the SAP-1 computer up to this point is as follows:

![ Figure 17 ](https://github.com/LincaMarius/ISAP-1_Computer_Proiect/blob/main/SAP-1_Computer_Analysis/Pictures/Figure17.png)

If we take into account that the memory is seen as a ROM memory during program execution, we obtain the following block diagram:

![ Figure 18 ](https://github.com/LincaMarius/ISAP-1_Computer_Proiect/blob/main/SAP-1_Computer_Analysis/Pictures/Figure18.png)

We can distinguish the three subsystems of the computer:
- The SAP-1 CPU
- The Memory Subsystem
- Inputs/Outputs Subsystem

They are interconnected through the three buses:
- 4-bit Address Bus
- 8-bit Data Bus
- 7-bit Control Bus

The available address space for the SAP-1 computer in this structure is:
- 16 bytes of Program Memory
- 1 Output Devices
