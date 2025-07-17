RISC-V ISA (Instruction set architecture)

![alt text](image-1.png)

RTL and HDL implementation depends on the architecture of the chip, which will therefore affect the final layout of the chip. 
Software to hardware pipeline
The OS takes input from software programs the user interfaces with. It compiles that information and converts it into an instruction set dependent on the chip architecture (can be RISC-V, ARM, x84 etc.). This instruction set is what we call assembly code. 

The assembler then takes this code and converts it into binary (machine language), which is then executed on the chip. 

![alt text](image-2.png)

PDKs (Process Design Kit)
Typically barred behind NDA due to it’s proprietary nature, there is now open source access due to the Skywater 130nm PDK. PDK can be considered as the interface between the designer and the foundry. 

PDKs can include:
- IO Libraries
- Process design rules
- Digital standard cell libraries
- Device models
- Etc.

ASIC Pipeline

![alt text](image-3.png)

Synthesis: This step converts RTL (Register Transfer Level) to circuitry using HDLs like verilog with standard cell libraries provided by a PDK. 

Floor and power planning: This step places power rails, logic gates, and other components. 

Placement: Done in two steps.

Global placement places the components where it thinks it may be most efficient, though this is definitely not the optimal placement. 

Detailed placement places the components in the more optimized positions after the initial global placement. 

Clock tree synthesis: There is a need to deliver clock and timing across the entire chip. Usually in the form of a free (H, X, Wishbone). Try to get minimum skew time with a clock tree. 

Signal routing: Uses available placement of wires to implement nets to connect cells together. 

Each metal layer is defined by the PDK: 
Pitch -> thickness of of tracks
Min width
Metal vias

(Sky130 lowest layer also called the local interconnect)

Sign off: 
DRC (Design rule checking)
LVS (Layout vs schematic)
Timing verification through STAOpenLane
OpenLane
This is software that facilitates a complete RTL to GDII pipeline. Many tools are used in this pipeline. 

![alt text](image-4.png)

How to run OpenLane (follow these steps)

![alt text]({0935160F-0298-4264-ACDB-3BF0560076ED}.png)

Yeah this is a convoluted method. You can just cd directly to the directory if you wanted to. 

To continue, run these commands in order:
docker (changes to bash-4.2$ shell)
Then
./flow.tcl -interactive
Then
package require openlane 0.9
Then
prep -design picorv32a

![alt text]({13521520-F93E-491F-9956-68170C59E6D8}.png)

The terminal looks like this once these steps are followed. 

Check the OpenLane GitHub repo for more info on commands to run. 

From here, we can initiate the process by typing in run_synthesis. This step may take a few minutes depending on your system. 

When the synthesis step is complete, there is a lot of information and data generated in the report. Using this, we can find the flop ratio. 

![alt text](image-5.png)

Flop ratio = # of d flip flops/# of cells * 100

In this case we have 14876 cells and 1613 d flip flops, so the ratio is 10.84.

