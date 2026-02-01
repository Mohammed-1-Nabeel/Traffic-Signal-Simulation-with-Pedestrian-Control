🚦6-Bit Sequential Traffic Light Controller
A discrete hardware implementation of a 4-way traffic management system. This project uses a 64-second cycle logic, controlled by a D-Flip-Flop-based counter and combinational logic gates to manage timing, yellow-phase transitions, and directional multiplexing.

🛠️ Hardware Logic Architecture
The system is driven by an NE555 Timer in Astable mode, providing the clock pulse to a 6-bit ripple/synchronous counter (Q0–Q5).

1. Timing Breakdown (64s Total Cycle)
Q0–Q1: Fine timing.

Q2–Q3: Used to detect the "Yellow" window.

Q4–Q5: State bits defining the active road (16 seconds per direction).

2. Yellow Phase Logic (The 12s–16s Window)
The system extracts a 4-second yellow signal within every 16-second phase. Since 12 
10
​
 =1100 
2
​
 , we obtain the signal via:

Yellow_Enable=Q3⋅Q2
This signal acts as a selector for the output MUX logic.

3. Directional Decoding
The higher-order bits Q5 and Q4 are decoded to ensure only one direction is active at a time:

Q5	Q4	Active Direction
0	0	North
0	1	South
1	0	East
1	1	West

Export to Sheets

4. Output Multiplexing (MUX)
Each road uses MUX-style logic to determine the active LED:

Green: Direction_Enable⋅ Yellow_Enable'
​
Yellow: Direction_Enable⋅Yellow_Enable

Red: Active whenever the Direction Enable is low.


🚀 Simulation Results
The logic ensures a Zero-Conflict transition. When Q4 and Q5 switch, the system instantly shifts the "Green/Yellow" logic to the next road, while the remaining three roads default to Red via the one-hot decoding.
