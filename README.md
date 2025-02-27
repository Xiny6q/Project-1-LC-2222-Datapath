Download link :https://programming.engineering/product/project-1-lc-2222-datapath/


# Project-1-LC-2222-Datapath
Project 1 – LC-2222 Datapath
Requirements

Download the proper version of CircuitSim. The proper version is version 1.8.2 or later. A copy of CircuitSim is available under Files on Canvas. You may also download it from the CircuitSim website (https://ra4king.github.io/CircuitSim/). In order to run CircuitSim, Java must be installed. If you are a Mac user, you may need to right-click on the JAR file and select “Open” in the menu to bypass Gatekeeper restrictions.

CircuitSim is still under development and may have unknown bugs. Please back up your work using some form of version control, such as a local/private git repository or Dropbox. Do not use public git repositories; it is against the Georgia Tech Honor Code.

The LC-2222 assembler is written in Python. If you do not have Python 2.6 or newer installed on your system, you will need to install it before you continue.

Project Overview and Description

Project 1 is designed to give you a good feel for exactly how a processor works. In Phase 1, you will design a datapath in CircuitSim to implement a supplied instruction set architecture. You will use the datapath as a tool to determine the control signals needed to execute each instruction. In Phases 2 and 3, you are required to build a simple finite state machine (the “control unit”) to control your computer and actually run programs on it.

Note: You will need to have a working knowledge of CircuitSim. Make sure that you know how to make basic circuits as well as subcircuits before proceeding. The TAs are always here if you need help.

Project 1 CS2200 – Computer Systems and Networks Fall 2023

Phase 1 – Implement the Datapath



Figure 1: Datapath for the LC-2222 Processor

In this phase of the project, you must learn the Instruction Set Architecture (ISA) for the processor we will be implementing. Afterwards, we will implement a complete LC-2222 datapath in CircuitSim using what you have just learned.

You must do the following:

Learn and understand the LC-2222 ISA. The ISA is fully specified and defined in Appendix A: LC-2222 Instruction Set Architecture. Do not move on until you have fully read and understood the ISA specification. Every single detail will be relevant to implementing your datapath in the next step.

Using CircuitSim, implement the LC-2222 datapath. To do this, you will need to use the details of the LC-2222 datapath defined in Appendix A: LC-2222 Instruction Set Architecture. You should model your datapath on Figure 1.

Put your name on your CircuitSim data path in a comment box so we know it is your work.

3.1 Hints

3.1.1 Subcircuits

CircuitSim enables you to break create reusable components in the form of subcircuits. We highly rec-ommend that you break parts of your design up into subcircuits. At a minimum, you will want to implement your ALU in a subcircuit. The control unit you implement in Phase 2 is another prime candidate for a subcircuit.

3.1.2 Debugging

As you build the datapath, you should consider adding functionality that will allow you to operate the whole datapath by hand. This will make testing individual operations quite simple. We suggest your datapath include devices that will allow you to put arbitrary values on the bus and to view the current value of the bus. Feel free to add any additional hardware that will help you understand what is going on.

Project 1 CS2200 – Computer Systems and Networks Fall 2023

3.1.3 Memory Addresses

Because of CircuitSim limitations, the RAM module is limited to no more than 16 address bits. Therefore, per our ISA, any 32-bit values used as memory addresses will be truncated to 16 bits (with the 16 most significant bits disregarded). If you use the RAM subcircuit we provide, this truncation has already been handled, and you can simply attach the 32-bit value from the MAR (Memory Address Register) to our custom RAM circuit. Otherwise, you will need to truncate the most significant bits of the the address value from the MAR before feeding it into the RAM.

3.1.4 Comparison Logic

The “Cmp Logic” box in Figure 1 is responsible for performing the comparison logic associated with the BLT, BGT, and BEQ instructions. The comparison logic should read the current value on the bus. When executing BLT, BGT, and BEQ, you should compute A − B using the ALU. While this result of the ALU is being driven on the bus, the comparison logic should read the result A − B and output a single “true” or “false” bit for either the condition A > B, A < B, or A == B depending on the instruction being executed.

Your comparison logic should be purely combinational. Feel free to use any CircuitSim components you wish to aid in your implementation.

3.1.5 Register File

You must implement your own register file. That is to say, you cannot use CircuitSim’s built-in RAM to create the register file. Consider what logic components you may want to use to implement addressing functionality (multiplexers, demultiplexers, decoders, etc). Your zero register must be implemented such that writes to it are ineffective, i.e., attempting to write a non-zero value to the zero register will do nothing. Do not forget to do this or you will lose points!

3.1.6 Register Select

From lecture and the textbook, you should be familiar with the “register select” (RegSel) multiplexer. The mux is responsible for feeding the register number from the correct field in the instruction into the register file. See Table 4 for a list of inputs your mux should have.

Phase 2 – Implement the Microcontrol Unit

In this phase of the project, you will use CircuitSim to implement the microcontrol unit for the LC-2222 processor. This component is referred to as the “Control Logic” in the images and schematics. The micro-controller will contain all of the signal lines to the various parts of the datapath.

You must do the following:

Read and understand the microcontroller logic:

Please refer to Appendix B: Microcontrol Unit for details.

Note: You will be required to generate the control signals for each state of the processor in the next phase, so make sure you understand the connections between the datapath and the microcontrol unit before moving on.

Implement the Microcontrol Unit using CircuitSim. The appendix contains all of the necessary in-formation. Take note that the input and output signals on the schematics directly match the signals marked in the LC-2222 datapath schematic (see Figure 1).

Project 1 CS2200 – Computer Systems and Networks Fall 2023

Phase 3 – Microcode and Testing

In this final stage of the project, you will write the microcode control program that will be loaded into the microcontrol unit you implemented in Phase 2. Then, you will hook up the control unit you built in Phase 2 of the project to the datapath you implemented in Phase 1. Finally, you will test your completed computer using a simple test program and ensure that it properly executes.

You must do the following:

Open and fill out microcode.xlsx file we’ve provided you (note: the formulas in the provided file will only work with Excel). You will need to mark which control signal is high (that is 1) for each of the states.

After you have completed all the microstates, convert the binary strings you just computed into hex and move them into the main ROM. You can just copy and paste the hex column (highlighted yellow) from the spreadsheet directly into the ROM component in Circuitsim. Do the same for the sequencer and condition ROMs.

Connect the completed control unit to the datapath you implemented in Phase 1. Using Figures 1 and 2, connect the control signals to their appropriate spots.

Finally, it is time to test your completed computer. Use the provided assembler (found in the “as-sembly” folder) to convert a test program from assembly to hex. For instructions on how to use the assembler and simulator, see README.txt in the “assembly” folder. Note: The simulator does not test your project, it simply provides a model. To test your design, you must load the assembled HEX into CircuitSim. We recommend using test programs that contain a single instruction since you are bound to have a few bugs at this stage of the project. Once you have built confidence, test your processor with the provided pow.s program as a more comprehensive test case.

Tips:

You can use the ”Clock Enabled” feature to start the clock, and you can also determine the clock frequency. Both are under ”Simulation” at the top.

There is a component in Debugging called Breakpoint. You can set a value and connect any wire to it. Then, once you start the clock, it will stop when the wire turns to the value you just set. You can connect it to your PC to stop at any instruction.

Autograder

The autograder for Project 1 mainly serves as a debugging tool, so there is no point assigned to it, and your final grade will not be determined by whether you pass the autograder or not. The autograder will execute the test program pow.s using your datapath and tell you which instruction goes wrong, but it won’t evaluate anything else. Feel free to use it as a tool to help you debug your circuit, but you won’t be able to rely on it entirely. As the autograder only tells you which instruction leads to an error, you must still figure out which part of your datapath is not functioning as expected. However, it should be easier to reproduce the error knowing the address of the failing machine instruction! If you want to use the autograder, you must follow a few rules:

Don’t rename the main subcircuit ”Datapath”

Name your PC register as “PC”

Name your IR register as “IR”

Name your state register as “State”

Name your 3 ROMs as ”MAIN”, ”SEQ”, and ”CC” respectively

Project 1 CS2200 – Computer Systems and Networks Fall 2023

Reference registers in regfile in lower case with prefixed $‘’ sign ($zero, $at, $v0…), according to Appendix A: LC-2222 Instruction Set Architecture.

Use only one clock globally, which means you should not use clock components in any subcircuits besides the main datapath. Instead, you should use an input pin and connect the clock signal to that subcircuit in the main datapath.

Use only one RAM as memory

In microcode, use the first row as your first state of FETCH macrostate.

Don’t change the layout of the microcode Excel sheet

If the autograder fails you, please first double-check if you meet all the rules above. If the autograder points you to a line of code, try to load the assembled HEX of the pow.s program into your RAM, clock it until PC turns to that line number, and check state by state to see if any component goes wrong when executing that instruction. Sometimes, you may not reproduce the error when you reach that instruction for the first time. This is because there are some loop structures and subroutine calls in the test program, and you will execute some instructions multiple times. The error occurs when you reach that instruction again and the condition changes (e.g. a conditional branch instruction).

When you get an error message, please first try to reproduce it locally and think about what you observe. If you still don’t know how to approach it, come to office hours or make a private post with a detailed explanation of your attempts of debugging, instead of just a post with the error message and a screenshot of your datapath. TAs won’t be able to help you solve the problem with that little amount of information.

Deliverables

To submit your project, you need to upload the following files to Gradescope:

CircuitSim datapath file (LC-2222.sim)

Microcode file (microcode.xlsx)

If you are missing one or both of those files, you will get a 0 so make sure that you have uploaded both of them.

Always re-download your assignment from Gradescope after submitting to ensure that all necessary files were properly uploaded. If what we download does not work, you will get a 0 regardless of what is on your machine.

This project will be demoed. In order to receive full credit, you must sign up for a demo slot and complete the demo. We will announce when demo times are released.

Project 1 CS2200 – Computer Systems and Networks Fall 2023

Appendix A: LC-2222 Instruction Set Architecture

The LC-2222 is a simple, yet capable computer architecture. The LC-2222 combines attributes of both ARM and the LC-2200 ISA defined in the Ramachandran & Leahy textbook for CS 2200.

The LC-2222 is a word-addressable, 32-bit computer. All addresses refer to words, i.e. the first word (four bytes) in memory occupies address 0x0, the second word, 0x1, etc.

All memory addresses are truncated to 16 bits on access, discarding the 16 most significant bits if the address was stored in a 32-bit register. This provides roughly 64 KB of addressable memory.

8.1 Registers

The LC-2222 has 16 general-purpose registers. While there are no hardware-enforced restraints on the uses of these registers, your code is expected to follow the conventions outlined below.

Table 1: Registers and their Uses

Register Number

Name

Use

Callee Save?

0

$zero

Always Zero

NA

1

$at

Assembler/Target Address

NA

2

$v0

Return Value

No

3

$a0

Argument 1

No

4

$a1

Argument 2

No

5

$a2

Argument 3

No

6

$t0

Temporary Variable

No

7

$t1

Temporary Variable

No

8

$t2

Temporary Variable

No

9

$s0

Saved Register

Yes

10

$s1

Saved Register

Yes

11

$s2

Saved Register

Yes

12

$k0

Reserved for OS and Traps

NA

13

$sp

Stack Pointer

No

14

$fp

Frame Pointer

Yes

15

$ra

Return Address

No

Register 0 is always read as zero. Any values written to it are discarded. Note: for the purposes of this project, you must implement the zero register. Regardless of what is written to this register, it should always output zero.

Register 1 is used to hold the target address of a jump. It may also be used by pseudo-instructions generated by the assembler.

Register 2 is where you should store any returned value from a subroutine call.

Registers 3 – 5 are used to store function/subroutine arguments. Note: registers 2 through 8 should be placed on the stack if the caller wants to retain those values. These registers are fair game for the callee (subroutine) to trash.

Registers 6 – 8 are designated for temporary variables. The caller must save these registers if they want these values to be retained.

Registers 9 – 11 are saved registers. The caller may assume that these registers are never tampered with by the subroutine. If the subroutine needs these registers, then it should place them on the stack and restore them before they jump back to the caller.

Register 12 is reserved for handling interrupts. While it should be implemented, it otherwise will not have any special use on this assignment.

Project 1 CS2200 – Computer Systems and Networks Fall 2023

Register 13 is the everchanging top of the stack; it keeps track of the top of the activation record for a subroutine.

Register 14 is the anchor point of the activation frame. It is used to point to the first address on the activation record for the currently executing process.

Register 15 is used to store the address a subroutine should return to when it is finished executing.

8.2 Instruction Overview

The LC-2222 supports a variety of instruction forms, only a few of which we will use for this project. The instructions we will implement in this project are summarized below.

Table 2: LC-2222 Instruction Set

31302928272625242322212019181716151413121110 9 8 7 6 5 4 3 2 1 0

ADD

0000

DR

SR1

unused

SR2

NAND

0001

DR

SR1

unused

SR2

ADDI

0010

DR

SR1

immval20

LW

0011

DR

BaseR

offset20

SW

0100

SR

BaseR

offset20

BEQ

0101

SR1

SR2

offset20

JALR

0110

RA

AT

unused

HALT

0111

unused

BLT

1000

SR1

SR2

offset20

LEA

1001

DR

unused

PCoffset20

BGT

1010

SR1

SR2

offset20

OR

1011

DR

SR1

unused

0

SR2

XOR

1011

DR

SR1

unused

1

SR2

8.2.1 Conditional Branching

Branching in the LC-2222 ISA is a bit different than usual. We have a set of branching instructions in-cluding BEQ, BLT, and BGT, which offer the ability to branch upon a certain condition being met. These instructions use comparison operators, comparing the values of two source registers. If the comparisons are true (for example, with the BGT instruction, if SR1 > SR2), then we will branch to the target destination of incrementedPC + offset20.

Project 1 CS2200 – Computer Systems and Networks Fall 2023

8.3 Detailed Instruction Reference

8.3.1 ADD

Assembler Syntax

ADD DR, SR1, SR2

Encoding

31302928272625242322212019181716151413121110 9 8 7 6 5 4 3 2 1 0

Project 1 CS2200 – Computer Systems and Networks Fall 2023

8.3.3 ADDI

Assembler Syntax

ADDI DR, SR1, immval20

Encoding

31302928272625242322212019181716151413121110 9 8 7 6 5 4 3 2 1 0

Project 1 CS2200 – Computer Systems and Networks Fall 2023

8.3.6 BEQ

Assembler Syntax

BEQ SR1, SR2, offset20

Encoding

31302928272625242322212019181716151413121110 9 8 7 6 5 4 3 2 1 0

Project 1 CS2200 – Computer Systems and Networks Fall 2023

8.3.9 BLT

Assembler Syntax

BLT SR1, SR2, offset20

Encoding

31302928272625242322212019181716151413121110 9 8 7 6 5 4 3 2 1 0

Project 1 CS2200 – Computer Systems and Networks Fall 2023

8.3.12 OR

Assembler Syntax

OR DR, SR1, SR2

Encoding

31302928272625242322212019181716151413121110 9 8 7 6 5 4 3 2 1 0

Project 1 CS2200 – Computer Systems and Networks Fall 2023

Appendix B: Microcontrol Unit

You will make a microcontrol unit which will drive all of the control signals to various items on the datapath. This Finite State Machine (FSM) can be constructed in a variety of ways. You could implement it with combinational logic and flip flops, or you could hard-wire signals using a single ROM. The single ROM solution will waste a tremendous amount of space since most of the microstates do not depend on the opcode or the conditional test to determine which signals to assert. For example, since the condition line is an input for the address, every microstate would have to have an address for condition = 0 as well as condition = 1, even though this only matters for one particular microstate.

To solve this problem, we will use a three ROM microcontroller. In this arrangement, we will have three

ROMs:

the main ROM, which outputs the control signals,

the sequencer ROM, which helps to determine which microstate to go at the end of the FETCH state,

and the condition ROM, which helps determine whether or not to branch during the BLT and BGT instructions.

Examine the following:



Figure 2: Three ROM Microcontrol Unit

As you can see, there are three different locations that the next state can come from: part of the output from the previous state (main ROM), the sequencer ROM, and the condition ROM. The mux controls which of these sources gets through to the state register. If the previous state’s “next state” field determines where to go, neither the OPTest nor ChkCmp signals will be asserted. If the opcode from the IR determines the next state (such as at the end of the FETCH state), the OPTest signal will be asserted. If the comparison circuitry determines the next state (such as in the BLT, BGT, or BEQ instructions), the ChkCmp signal will be asserted. Note that these two signals should never be asserted at the same time since nothing is input into the “11” pin on the MUX.

Project 1 CS2200 – Computer Systems and Networks Fall 2023

The sequencer ROM should have one address per instruction, and the condition ROM should have one address for condition true and one for condition false.

Before getting down to specifics you need to determine the control scheme for the datapath. To do this examine each instruction, one by one, and construct a finite state bubble diagram showing exactly what control signals will be set in each state. Also determine what are the conditions necessary to pass from one state to the next. You can experiment by manually controlling your control signals on the bus you’ve created in Phase 1 – Implement the Datapath to make sure that your logic is sound.

Once the finite state bubble diagram is produced, the next step is to encode the contents of the Control Unit ROM. Then you must design and build (in CircuitSim) the Control Unit circuit which will contain the three ROMs, a MUX, and a state register. Your design will be better if it allows you to single step and ensure that it is working properly. Finally, you will load the Control Unit’s ROMs with the hexadecimal generated by your filled out microcode.xlsx.

Note that the input address to the ROM uses bit 0 for the lowest bit of the current state and 5 for the highest bit for the current state.

Table 3: ROM Output Signals

Bit

Purpose

Bit

Purpose

Bit

Purpose

Bit

Purpose

Bit

Purpose

0

NextState[0]

6

DrREG

12

LdPC

18

WrREG

24

OPTest

1

NextState[1]

7

DrMEM

13

LdIR

19

WrMEM

25

ChkCmp

2

NextState[2]

8

DrALU

14

LdMAR

20

RegSel[0]

3

NextState[3]

9

DrALU2

15

LdA

21

RegSel[1]

4

NextState[4]

10

DrPC

16

LdB

22

ALU[0]

5

NextState[5]

11

DrOFF

17

LdCmp

23

ALU[1]

Table 4: Register Selection Map

RegSel[1]

RegSel[0]

Register

0

0

RX (IR[27:24])

0

1

RY (IR[23:20])

1

0

RZ (IR[3:0])

1

1

unused

Table 5: ALU Function Map

ALU[1]

ALUl[0]

Function

0

0

ADD

0

1

SUB

1

0

NAND

1

1

A + 1

