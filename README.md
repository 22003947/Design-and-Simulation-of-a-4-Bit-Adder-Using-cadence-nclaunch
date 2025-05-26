## Ex No: 07 - Design and Simulation of a 4-Bit Adder Using Verilog and Cadence nclaunch

## Aim
The aim is to design and simulate a **4-bit Adder** using **Verilog HDL** and verify its functionality using **Cadence nclaunch** for simulation.

---

## Tools Required
### Cadence EDA Suite
- **nclaunch** (for functional and timing simulation)

### Hardware Requirements
- Minimum **4GB RAM** and a **multi-core processor**

---

## Procedure

### 1. Writing Verilog Code:
- Create a new Verilog module for the **1-bit Full Adder**.
- Implement a **ripple carry adder** using **four 1-bit full adders** to form a **4-bit Adder**.
- Define input ports (**A[3:0], B[3:0], Cin**) and output ports (**Sum[3:0], Cout**).

### 2. Simulation Using Cadence nclaunch:
- Open **nclaunch** and load the Verilog file.
- Compile the design and check for **syntax errors**.
- Write a **testbench** to apply different input combinations.
- Run the **simulation** and observe the **waveforms**.
- Verify that the output sum and carry are correct for all cases.

---

## Verilog Code for 1-Bit Full Adder
```verilog
module full_adder (
    input A, B, Cin,
    output Sum, Cout
);
    assign Sum = A ^ B ^ Cin;
    assign Cout = (A & B) | (B & Cin) | (A & Cin);
endmodule
```

## Truth Table for 1-Bit Full Adder

![image](https://github.com/user-attachments/assets/0ea58111-49fb-49a4-ad6a-ee36cbf4e479)

## Verilog Code for 4-Bit Ripple carry Adder
```verilog
module adder_4bit (
    input [3:0] A, B,
    input Cin,
    output [3:0] Sum,
    output Cout
);
    wire C1, C2, C3;

    full_adder FA0 (A[0], B[0], Cin, Sum[0], C1);
    full_adder FA1 (A[1], B[1], C1, Sum[1], C2);
    full_adder FA2 (A[2], B[2], C2, Sum[2], C3);
    full_adder FA3 (A[3], B[3], C3, Sum[3], Cout);
endmodule
```
## Verilog Testbench Code for 1-Bit Full Adder
```verilog
module tb_adder_4bit;
    reg [3:0] A, B;
    reg Cin;
    wire [3:0] Sum;
    wire Cout;

    // Instantiate the 4-bit adder
    adder_4bit UUT (
        .A(A), .B(B), .Cin(Cin),
        .Sum(Sum), .Cout(Cout)
    );

    initial begin
               
        // Test cases
        A = 4'b0000; B = 4'b0000; Cin = 0; #10;
        A = 4'b0011; B = 4'b0101; Cin = 0; #10;
        A = 4'b1111; B = 4'b0001; Cin = 0; #10;
        A = 4'b1010; B = 4'b0101; Cin = 1; #10;
        A = 4'b1111; B = 4'b1111; Cin = 1; #10;

        $finish;
    end
endmodule

```

## Truth Table for 4-Bit Full Adder

![image](https://github.com/user-attachments/assets/567af4cf-875d-448b-b616-40e450d5bbde)


## Simulation Results

### Nclaunch Work Library Window

![Screenshot 2025-05-21 155538](https://github.com/user-attachments/assets/187ebe28-40e2-44b2-9b78-d08bdc67d62c)

### Simulation Waveforms
![Screenshot 2025-05-21 155512](https://github.com/user-attachments/assets/4d1457be-ef30-4b8b-a58d-aa8ac39c078c)



## Results
Successfully designed the 1-bit Full Adder and 4-bit Adder using Verilog HDL.
Simulated the design using Cadence nclaunch and verified the output.
Observed correct addition functionality for all test cases.


