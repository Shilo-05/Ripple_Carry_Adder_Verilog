# Ripple_Carry_Adder_Verilog

```
RIPPLE CARRY ADDER USING VERILOG - QUARTUS
```

```
Developed By: Oswald Shilo
Reg No: 212223040139
Sub: Digital Electronics
```

### Ripple Carry Adder in Verilog

#### 1. Overview
- A Ripple Carry Adder (RCA) is a basic arithmetic circuit used to add two binary numbers.
- It is composed of multiple **Full Adders** connected in sequence.
- The carry-out from one full adder propagates ("ripples") to the next.

---

#### 2. Full Adder Logic
- A **Full Adder** adds three inputs:
  - Two binary bits: `A` and `B`.
  - One carry-in: `Cin`.
- Outputs:
  - - **Sum (`S`)**: `S = A ⊕ B ⊕ Cin` (XOR operation).
  - - **Carry-out (`Cout`)**: `Cout = (A ⋅ B) + (Cin ⋅ (A ⊕ B))` (AND and OR operations).
  
---

#### 3. Ripple Carry Adder (N-Bit)
- For an **N-bit RCA**, N full adders are connected in sequence.
- The carry-out from each full adder serves as the carry-in for the next.

---

#### 4. Verilog HDL Code
##### **a) Full Adder Module**
```verilog
module full_adder (A, B, Cin, Sum, Cout);
    input A, B, Cin;            // Inputs: A, B, Carry-in
    output Sum, Cout;           // Outputs: Sum, Carry-out
    assign Sum = A ^ B ^ Cin;   // XOR logic for sum
    assign Cout = (A & B) | (Cin & (A ^ B)); // Carry logic
endmodule
```
- **Purpose**: Implements the single-bit full adder logic.
- **Inputs**: `A`, `B`, `Cin`.
- **Outputs**: `Sum`, `Cout`.

##### **b) Ripple Carry Adder Module (4-bit)**
```verilog
module RP2 (A, B, Cin, Sum, Cout);
    input [3:0] A, B;      // 4-bit binary inputs A and B
    input Cin;             // Initial carry-in
    output [3:0] Sum;      // 4-bit sum output
    output Cout;           // Final carry-out
    wire C1, C2, C3;       // Internal carry signals

    // Instantiate 4 Full Adders
    full_adder FA0 (A[0], B[0], Cin, Sum[0], C1);  // LSB Full Adder
    full_adder FA1 (A[1], B[1], C1, Sum[1], C2);  // Second Bit Full Adder
    full_adder FA2 (A[2], B[2], C2, Sum[2], C3);  // Third Bit Full Adder
    full_adder FA3 (A[3], B[3], C3, Sum[3], Cout); // MSB Full Adder
endmodule
```
- **Purpose**: Implements a 4-bit Ripple Carry Adder using the `full_adder` module.
- **Inputs**:
  - `A[3:0]`, `B[3:0]`: Two 4-bit numbers to add.
  - `Cin`: Initial carry-in.
- **Outputs**:
  - `Sum[3:0]`: 4-bit sum result.
  - `Cout`: Final carry-out.
- **Internal Wires**:
  - `C1`, `C2`, `C3`: Intermediate carry signals between full adders.
  
---

#### 5. Structural-Level Explanation
- **Instantiation**:
  - The `RP2` module uses **structural modeling** by instantiating the `full_adder` module multiple times.
- **Carry Propagation**:
  - The `Cout` of one full adder is connected to the `Cin` of the next full adder, forming the ripple chain.
- **Hierarchy**:
  - The design is modular and scalable for higher bit widths.

---

### Explanation
- The code demonstrates a **structural modeling approach** to design a Ripple Carry Adder.
- It consists of:
  - A **single-bit Full Adder** module for addition logic.
  - A **4-bit Ripple Carry Adder** module that chains 4 full adders to create a complete circuit.


#### Output

![image](https://github.com/user-attachments/assets/c18de595-43d1-4faa-8632-526d7eb4c34d)



![image](https://github.com/user-attachments/assets/933b7ad2-ef3e-4105-92af-10e177d89f0a)


#### RTL VIEWER


![image](https://github.com/user-attachments/assets/7f780264-81c9-4df9-b3b9-694f3bf5b4ad)

### Conclusion

The Ripple Carry Adder (RCA) is a simple and modular circuit for binary addition, using full adders in sequence. It is easy to implement but has limitations due to carry propagation delay. The Verilog design showcases a scalable approach for adding binary numbers.
