AUV_Power_Redundancy
AUV Power Redundancy Circuit (LM5050 Ideal Diode)

This is my project for the AUV electronics team task. The goal is to build a dual-input power redundancy circuit. It lets the AUV switch between two power sources (like a main battery and a backup) automatically, making sure power doesn't flow backward into the wrong source while keeping the voltage drop as low as possible.

Instead of regular diodes, I'm using an ideal diode controller setup because normal diodes drop too much voltage and waste a lot of power as heat.

What the Circuit Does
With datasheet reference , two LM5050-1 controllers (one for each power rail) driving two external N-channel MOSFETs. The controllers sense the voltage across the MOSFETs. If one supply drops or a reverse voltage happens, the chip turns off the MOSFET gate immediately to block reverse current. Both rails meet at a shared output bus that connects to the rest of the AUV systems.

Component Selection & Footprints

I chose the following parts and footprints based on our project requirements
Controller: LM5050-1 (U1, U2)
Footprint: Package_TO_SOT_SMD:SOT-23-6
This is the standard surface-mount package for this chip. It’s small enough for a compact board but still manageable to solder.

2. Pass Elements: N-Channel MOSFETs (Q1, Q2)
Footprint: Package_TO_SOT_SMD:SOT-23
Why: I selected a basic SOT-23 N-channel MOSFET for this layout. The logic behind using an N-channel FET here is that it sits on the high side with its Source on the input supply side and Drain on the output side. When the LM5050 pumps up the gate voltage, the MOSFET turns fully on, giving us an incredibly low RDS(on) (internal resistance). 

3. Passives & Connectors
Resistor & Capacitor (R1, C1): SMD:C_0805_2012Metric . I went with 0805 packages because they are the perfect for a beginner—small enough to keep the board compact, but easy enough to hand-solder without losing them with tweezers.
Connectors (J1, J2, J3):Connector_PinHeader_2.45mm:PinHeader_1x02_P2.54mm_Vertical. Standard 2-pin headers used for the power inputs and the main output.

Design Fixes I Made Along the Way
While setting up the schematic, I ran into a few issues that I had to fix:
The MOSFET Orientation: At first, the pin mappings were a bit confusing, but I fixed it so that the Source goes to the input supply and the Gate is driven safely by Pin 5 (GATE) of the LM5050.

Git Workflow
I used Git branches to make sure I didn't ruin my working schematic while fixing things.
Kept updating my changes by first running ERC and then commiting the changes to Git . 
First made the schematic , then footprint selection and then designined pcb layout by placing componenets and routing, added a gorund pad as base to overcome grounding errors .
Finally updates all changes to git and committed .
