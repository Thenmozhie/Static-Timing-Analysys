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

Standard Parasitic Exchange format (SPEF)


