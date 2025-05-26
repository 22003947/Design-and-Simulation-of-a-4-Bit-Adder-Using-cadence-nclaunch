# Ex No: 07 - Design and Simulation of a 4-Bit Adder Using Verilog and Cadence nclaunch

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

![447001839-6580d034-e392-4fd6-be6f-168834a2af56](https://github.com/user-attachments/assets/a7ecfb1a-6e93-4a39-b52b-7a3c573e5e9d)


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

![444656676-567af4cf-875d-448b-b616-40e450d5bbde](https://github.com/user-attachments/assets/623da1bd-07e3-46d3-8cc4-e7a473647041)



## Simulation Results

### Nclaunch Work Library Window

![446033351-187ebe28-40e2-44b2-9b78-d08bdc67d62c](https://github.com/user-attachments/assets/7839e55e-b069-4be6-9611-ea8b14ef55d2)


### Simulation Waveforms
![447001839-6580d034-e392-4fd6-be6f-168834a2af56](https://github.com/user-attachments/assets/0ead4da3-4208-49f2-ad9a-9cf251eab544)




## Results
Successfully designed the 1-bit Full Adder and 4-bit Adder using Verilog HDL.
Simulated the design using Cadence nclaunch and verified the output.
Observed correct addition functionality for all test cases.


