# Exp-7--Upcounter
# Design and Verification of a 4-bit Synchronous Up-Counter
## Aim
To design and verify a 4-bit Synchronous Up-Counter using Verilog HDL, and to observe its behaviour using a testbench and VCD waveform.

## Theory / Synopsis
A synchronous up-counter is a sequential circuit whose output increments by one on every active edge of a common clock, all flip-flops being clocked together (hence 'synchronous', as opposed to a ripple counter where each stage clocks the next). Here a 4-bit counter is realized, so the count cycles through 0000 to 1111 (0 to 15 in decimal) and then wraps around (overflows) back to 0000.

An enable input (en) is included so that the counter only increments when en = 1 and simply holds its value when en = 0. An active-high asynchronous reset clears the count to zero irrespective of the clock.

## Functional Description

On every rising edge of clk:

if (rst) count <= 4'b0000;

else if (en) count <= count + 1;   // increments, wraps 1111 -> 0000

else count <= count;                // holds present value

## Design / RTL Program

<img width="1246" height="487" alt="exp7 (2)" src="https://github.com/user-attachments/assets/1dbeee6b-3e49-4b0b-924c-2acb3044056f" />

## Testbench Program
<img width="1556" height="1028" alt="exp7 (1)" src="https://github.com/user-attachments/assets/e52e5bcf-f2d2-487e-b348-1444353b3f91" />


## Operation / Truth Table

State transition (en = 1, rst = 0 unless noted)

<img width="406" height="205" alt="image" src="https://github.com/user-attachments/assets/f67141a6-9926-4baa-b4fc-af002e8f4824" />

## Simulation Procedure

STEP 1 – Open Terminal
Open a terminal in the experiment folder. 

STEP 2 – Load Synopsys Environment
source /synopsys/start.sh

STEP 3 – Compile Using VCS
vcs up_counter.v tb.v -full64
If compilation is successful, VCS generates the simulation executable:
simv

STEP 4 – Run Simulation
./simv
The terminal displays the reset, clock, enable and the resulting count value (in binary and decimal) at every change (via $monitor). A VCD waveform file is also generated:
up_counter.vcd

STEP 5 – Open DVE
dve -full64
Other option:
dve -full64 &
A DVE environment will open.

## DVE Waveform Verification

In DVE:

●	Open the testbench hierarchy.

●	Locate the signals: clk, rst, en, count[3:0].

●	Add the signals to the waveform window.

●	Run / inspect the waveform.

●	Verify that count increments by 1 on every rising edge of clk while en = 1 and rst = 0.

●	Verify that count holds its present value whenever en = 0.

●	Confirm that count wraps from 1111 back to 0000 after the 16th enabled clock edge (overflow).

●	Confirm that count resets to 0000 immediately whenever rst = 1, independent of clk.

The waveform should agree with the state transition table.

## Expected Result

The 4-bit Synchronous Up-Counter was realized using Verilog HDL, with the characteristic behaviour:

count(next) = count + 1   (when en = 1), wrapping from 1111 to 0000

The design was compiled and simulated using Synopsys VCS, and the functionality was verified using DVE waveform analysis, matching the expected state transition table.

## Output

<img width="1685" height="430" alt="exp7 (3)" src="https://github.com/user-attachments/assets/7617f4b2-a810-49f6-81a2-0f1b2487d2a4" />

## Result

Thus, the 4-bit Synchronous Up-Counter was designed, implemented using Verilog HDL, successfully simulated using Synopsys VCS, and verified using Synopsys DVE.

