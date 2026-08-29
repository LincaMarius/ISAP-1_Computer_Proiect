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

![ Figure 1 ](https://github.com/LincaMarius/ISAP-1_Computer_Proiect/blob/main/Pictures/Figure1.png)

### More detailed Block Diagram
I studied the original schematic of the SAP-1 Computer and recreated the block diagram to represent the actual functional blocks as closely as possible and I present it in the following figure:

![ Figure 2 ](https://github.com/LincaMarius/ISAP-1_Computer_Proiect/blob/main/Pictures/Figure2.png)

The HLT control signal was omitted in the original Block Diagram.
