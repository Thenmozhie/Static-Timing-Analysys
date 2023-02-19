# Static-Timing-Analysys
OpenSTA
OpenSTA is a static analysis tool, used to verify the timing of the design. Incremental updating of delays, arrivals, and required times are done using queries.
This analysis provides timing checks -from, -through, -to, multiple paths to endpoint, delay calculation and also checks timing setup 
Following image shows the steps involved to open Lab1,
  
Simple.v is our design file. The file ‘sky130_fd_sc_hd_tt_025C_1v80.lib’ include library cell information and inside this file, we have cell named ‘sky130_fd_sc_hd__nand2_1’ which is used in our design (simple.v).
 
 
Run file,
 
Constraints creation:
Sdc file,
 
Execution of run file (run.tcl),
 
Output: 
Slack should always be positive (meeting the time), If slack is negative, then we need to fix the issue.
 
 
