# Project-Based-Experiment
# DE-WorkShop
### 1. Full Adder Design:

The design utilizes a full adder component as the building block for the RCA.
A full adder takes three binary inputs (X, Y, and Ci) and generates two outputs: the sum (S) and carry-out (Co).
The logic uses XOR gates to compute the sum and carry based on the input bits.

### 2. Ripple Carry Adder Design:

The RCA consists of four full adders connected in cascade.
Each full adder adds two corresponding bits from the input operands (X and Y) along with the carry-in (Ci) from the previous stage.
The carry-out (Co) of one stage becomes the carry-in (Ci) for the next stage, hence the name "ripple carry."
The first stage's carry-in (Ci) is typically set to 0.

### 3. Verilog Code Breakdown:

The ripple_adder module:
Takes two 4-bit inputs (X and Y).
Instantiates four fulladder modules, one for each bit position.
Connects the corresponding bits from X and Y to each full adder.
Sets the carry-in (Ci) of the first full adder to 0.
The outputs of each full adder (sum and carry-out) are chained together to form the final 4-bit sum (S) and carry-out (Co) of the RCA.
The fulladder module:
Takes three 1-bit inputs (X, Y, and Ci).
Uses XOR gates to perform the sum and carry logic based on the truth table of a full adder.
Algorithm (for conceptual understanding, not actual code):

For each bit position (i=0 to 3):
Add the corresponding bits from X[i] and Y[i].
Include the carry-in (Ci) from the previous stage (or 0 for the first stage).
Based on the full adder logic:
Compute the sum (S[i]) of the three bits.
Generate the carry-out (Co) for the next stage.
The final sum (S) is the collection of all the individual bit sums (S[i]).
The final carry-out (Co) is the carry-out from the last full adder stage.

**Developed by :** Paida ram sai

**Reference No :** 212223110034

## PROGRAM :


module ripple_adder(X, Y, S, Co);
  input [3:0] X, Y;
  output [3:0] S;
  output Co;
  wire w1, w2, w3;

  // Instantiate 4 full adders
  fulladder u1(X[0], Y[0], 1'b0, S[0], w1);
  fulladder u2(X[1], Y[1], w1, S[1], w2);
  fulladder u3(X[2], Y[2], w2, S[2], w3);
  fulladder u4(X[3], Y[3], w3, S[3], Co);
endmodule

module fulladder(X, Y, Ci, S, Co);
  input X, Y, Ci;
  output S, Co;
  wire w1, w2, w3;

  xor G1(w1, X, Y);
  xor G2(S, w1, Ci);
  and G3(w2, w1, Ci);
  and G4(w3, X, Y);
  or G5(Co, w2, w3);
endmodule

## RTL VIEWER :

![image](https://github.com/PuliNagaNeeraj/DE-WorkShop/assets/138849173/6a0221a1-51a3-433b-940d-3882aefbee37)

## RESULT :

Thus the design leverages the full adder functionality to achieve a 4-bit binary addition using a ripple carry approach.
