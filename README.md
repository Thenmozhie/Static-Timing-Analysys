# Static-Timing-Analysys
DAY1

STA is the method of verifying timing performance of a design. It does not use test benches and does not check the functionality. It uses mathematical techniques instead of input vectors. Inputs to STA are gate level netlist, constraints file and logical libraries (delays, transition time, etc.,). STA breaks the design at ports and sequential elements (Path can be FF to port(I/O), FF to FF or port to FF). Timing elements includes, start point (usually input ports or reg clock pins), end point (usually output ports or reg data pins). Setup and hold time: The minimum amount of time, the data should be available(stable) at the input of sequential circuit before clock edge in the data path is called setup time. This enforces maximum delay. The minimum amount of time, the data should be stable at the input of sequential device after clock edge that captures data. This enforces minimum delay.

Setup slack calculation,
Setup slack = data required time – data arrival time
Arrival time should always be less than the required time. Slack value should be positive. If we get negative value, then we need to fix.

OpenSTA - LAB1

OpenSTA is a static analysis tool, used to verify the timing of the design. Incremental updating of delays, arrivals, and required times are done using queries.
This analysis provides timing checks -from, -through, -to, multiple paths to endpoint, delay calculation and also checks timing setup 
Following image shows the steps involved to open Lab1,
![image](https://user-images.githubusercontent.com/87753795/219973001-4d2ff094-fcff-4fb6-9924-db8d259c5b77.png)
 
Simple.v is our design file. The file ‘sky130_fd_sc_hd_tt_025C_1v80.lib’ include library cell information and inside this file, we have cell named ‘sky130_fd_sc_hd__nand2_1’ which is used in our design (simple.v).
![image](https://user-images.githubusercontent.com/87753795/219973009-6402df61-b89f-458e-ae5c-1c8ec5bbce16.png)
![image](https://user-images.githubusercontent.com/87753795/219973018-47bc0f1d-aec4-49bc-bc3c-051cc8970344.png)

Run file,
![image](https://user-images.githubusercontent.com/87753795/219973029-73178340-616f-4edc-9767-2ea994264c35.png)
Constraints creation:
Sdc file,
![image](https://user-images.githubusercontent.com/87753795/219973046-8e1ed088-7861-4d71-9582-351f4badb714.png)

Execution of run file (run.tcl),
![image](https://user-images.githubusercontent.com/87753795/219973051-5f4d4a4e-8717-4b75-aaa4-2c667b682fb0.png)

Output: 
Slack should always be positive (meeting the time), If slack is negative, then we need to fix the issue.
![image](https://user-images.githubusercontent.com/87753795/219973071-b6b41ca3-72ef-46b6-8272-fb69016168a2.png)
![image](https://user-images.githubusercontent.com/87753795/219973079-aa283bb1-a1ce-43d9-a533-a7b9ad39518b.png)

 DAY 2
 
Apart from setup and hold check, there are also other timing checks such as clock gating checks (happens on enable clk pin w.r.t clk), asyn pin check (ensure when the reset can de-assert w.r.t clk), data to data checks (between two skews there should be certain time). STA provides some design rule checks such as slew/transition analysis, Load analysis, clock skew analysis, pulse width check.

Slew/transition analysis:
Rise slew is the time taken by the signal when it rises from 30% Vdd to 70% Vdd. Fall slew is the time taken to fall from 70% Vdd to 30% Vdd (from logic 0 to 1). We can specify specific constraints in order to ensure that these slew values have max and min values. In this analysis, STA will check whether the slew values are maintained throughout the design. 
Load Analysis: We can specify min and max capacitance on ports and nets, fanout loads on ports and I/O pins.
Clock Skew analysis: It's also important to consider the skew between the launch and capture clock waveforms; the skew is positive if the capture flop clock leads the launch flop clock and the skew is negative if the launch clock leads the capture clock.
Latch Timing: 
In flops, the data is launched and captured at the edges, whereas latched based designs allow more flexibility in timing. Data will be accepted at any time before the latch closes. Time borrowing is possible in latch. If one logic has more delay and other logic has less delay, then the time is borrowed from the logic which has less delay (next clock cycle).

![image](https://user-images.githubusercontent.com/87753795/220012673-a06ab667-a0c3-458a-9485-06d1b7c38904.png)


STA Text Report Evaluation:
STA tool will convert gate level representation to node and arc level representation. The diagram shows the discription of timing analysis report.
 
 ![image](https://user-images.githubusercontent.com/87753795/220012709-1bdc791c-4ccd-435e-b21b-c758e3dd9e94.png)

Lab 2
1.	No of cells in simple_max file: 
Ans: 211 (INV (X,Y,Z) = 30 + NAND2,NAND3,NAND4(X,Y,Z) = 120 + NOR2,NOR3,NOR4 (X,Y,Z) = 120, DFF_X80 = 1)
2.	Pins of cell NAND2_X1:
Ans: 3 (Pin o,a,b)
3.	Difference between NAND2_X1 and NAND3_X1
Ans: NAND2_X1 – Capacitance value is 6.40
NAND3_X1 – Capacitance value is 4.27
4.	Difference between simple_min.lib and simple_max.lib
Ans: Fabrication process variations could either increase or decrease the delay of a cell. So, we need to set early and late value while setting the derate factor. STA tool would consider early or late timing derate based on the path and type of analysis.

Standard Parasitic Exchange format (SPEF):

Describes parasitic information (electronic info like connectivity, capacitance, resistance and Inductance) of the design.
SPEF file has 4 main sections, header, name map, top level ports, parasitic description.

![image](https://user-images.githubusercontent.com/87753795/220014306-14cc4e1d-01b3-45db-8ac4-bb1853df7326.png)

DAY 3:
Multiple clock:
When there are multiple clocks with different frequencies, setup check is calculated by expanding the clock to common base period. STA used the most restrictive setup time. There are two rules for hold check. Rule1: Data launched at setup launch edge must not be captured by previous capture edge. Rule2: Data launched at next launch edge must not be captured by current setup capture edge.

Timing Arc and Timing Sense:
Timing arcs are of two types, 1- cell arcs (input to output), 2- net arcs (one cell to another cell).

 ![image](https://user-images.githubusercontent.com/87753795/220229384-2cc90164-ed0f-4fcf-9764-de719e79cf41.png)

Sequential arcs:

 ![image](https://user-images.githubusercontent.com/87753795/220229410-582b2d40-a66f-49b5-9397-3826abcfb343.png)

Combinational Arcs:
Input A is connected to output and input B is connected to output and no state element is involved.

Relation between combinational/sequential/cell and net arcs:
Combinational arcs: Combinational arcs represent the propagation delay of signals through the logic gates and are typically modeled as logical functions or Boolean expressions. Combinational arc is where data can propagate combinational without needing any enabling signal typically clock. 

Cell Arc: A cell arc represents the delay through a single logic cell or gate, such as an AND gate or an inverter. Cell arcs are typically characterized by the delay of the cell for different input combinations and are used in the delay calculation of the combinational arcs. In STA, both types of delays are used to analyze the timing behavior of a digital circuit. So, a cell arc can be both combinational or sequential and sometimes both for complex cells

Combinational delays are used to calculate the critical path delay, while cell delays are used to calculate the delay of individual gates or cells in the circuit. The critical path is the longest path of combinational logic that determines the maximum operating frequency of the circuit.

Combinational arcs in Static Timing Analysis include the net delays between sequential elements and the combinational logic that connects them. Cell arcs, on the other hand, are a subset of combinational arcs and refer to the delay through a single logic cell or gate. 

In other words, a combinational arc represents the delay through the entire path that connects two sequential elements, which includes the delays of all the logic gates and wires in the path. The delay of a combinational arc is the sum of the cell delays of all the gates along the path, as well as the delay of the wires that connect the gates.

Cell arcs are used to model the delay of individual gates or cells in the circuit, and are a key component of the delay calculation for the combinational arcs. The cell delay is typically measured by characterization, which involves measuring the delay of the gate or cell for different input patterns and loading conditions. So, while cell arcs are a subset of combinational arcs, they are also distinct in that they represent the delay through a single gate or cell, whereas a combinational arc represents the delay through an entire path of logic gates and wires.

Timing sense: Positive unate arc (output follows input), Negative unate arc (output followes the input in opposite direction), Non-unate arc (when we can’t predict if the output is going to follow the input or not).

Cell Delays:
Cell delays calculations are the function of input transition (propagation delay), output load/capacitance.

Positive clock slew: Capture clock delay is more. This skew helps in making the time to meet setup time.
Negative clock skew: Capture clock delay is less. Less time window to meet setup time.
Clock latency: clock source latency, network latency.

Clock jitter: Practically, there will be more uncertainty in clock edges.
![image](https://user-images.githubusercontent.com/87753795/220229444-02bbb132-88ab-4c6d-9fc0-b43fdfe67d16.png)

Setup and hold in detained:
Setup check:
![image](https://user-images.githubusercontent.com/87753795/220229462-c0eeb6c1-498a-43e2-a03d-b87f76a86bc8.png)

Setup check : Tc2q + Tcomb + Tsetup <= TPeriod + Tskew - Su
Su = setup clock uncertainity

Hold Check: Tc2q + Tcomb + Tsetup >= TPeriod + Tskew + Hu
Hu = hold clock uncertainty

Different Delay value on path – setup check: Path delay can have min, max or nominal value. STA to make setup pessimistic, uses max delay value on data path in launch side and min delay value in capture side.

Different Delay value on path – hold check: STA uses min delay value on data path in launch side and max delay value in capture side.

Lab 3:
Understanding slack calcuation,
![image](https://user-images.githubusercontent.com/87753795/220229476-75b3789e-f01a-43f9-9a36-418c5bee3dc8.png)

After running the above run file, the following slacks are obtained,

![image](https://user-images.githubusercontent.com/87753795/220229498-d28dca0c-3512-4e92-831d-a23091d669c5.png)





