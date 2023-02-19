# Static-Timing-Analysys
OpenSTA
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

 
