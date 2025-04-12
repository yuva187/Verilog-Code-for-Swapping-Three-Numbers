# Verilog-Code-for-Swapping-Three-Numbers
## Aim
To design and simulate a Verilog HDL code for swapping the values of three numbers without using any temporary variables, and verify the correctness of the swapping operation through a testbench using the Vivado 2023.1 simulation environment.

## Apparatus Required
Vivado 2023.1 or equivalent Verilog simulation tool.

## Procedure
Launch Vivado 2023.1:

Open Vivado and create a new project.
Write the Verilog Code for Swapping:

Write the Verilog code that swaps the values of three numbers (a, b, and c) using basic arithmetic or bitwise operations without using temporary variables.
Create the Testbench:

Write a testbench to simulate the swapping operation. The testbench should initialize three numbers, trigger the swapping module, and check if the values are swapped correctly.
Add the Verilog Files:

Add the Verilog module and the testbench file to the Vivado project.
Run Simulation:

Run the behavioral simulation in Vivado to verify the swapping operation.
Observe the Waveforms:

Examine the waveform to confirm that the values of the three numbers are swapped as expected.
Save and Document Results:

Capture the waveform output and include the results in your report for verification.

## Verilog Code:
## Blocking:
```


module swap_three (
    input  [7:0] a_in,
    input  [7:0] b_in,
    input  [7:0] c_in,
    output [7:0] a_out,
    output [7:0] b_out,
    output [7:0] c_out
);

assign a_out = b_in;
assign b_out = c_in;
assign c_out = a_in;

endmodule

//Test Bench Blocking

module swap_three_tb;

    // Inputs
    reg [7:0] a_in;
    reg [7:0] b_in;
    reg [7:0] c_in;

    // Outputs
    wire [7:0] a_out;
    wire [7:0] b_out;
    wire [7:0] c_out;

    // Instantiate the Unit Under Test (UUT)
    swap_three uut (
        .a_in(a_in),
        .b_in(b_in),
        .c_in(c_in),
        .a_out(a_out),
        .b_out(b_out),
        .c_out(c_out)
    );

    initial begin
        // Display header
        $display("Time\t a_in b_in c_in => a_out b_out c_out");

        // First test case
        a_in = 8'd10;
        b_in = 8'd20;
        c_in = 8'd30;
        #10;
        $display("%0dns\t %d   %d   %d   => %d    %d    %d", 
                  $time, a_in, b_in, c_in, a_out, b_out, c_out);

        // Second test case
        a_in = 8'd5;
        b_in = 8'd15;
        c_in = 8'd25;
        #10;
        $display("%0dns\t %d   %d   %d   => %d    %d    %d", 
                  $time, a_in, b_in, c_in, a_out, b_out, c_out);

        // Third test case
        a_in = 8'd100;
        b_in = 8'd200;
        c_in = 8'd255;
        #10;
        $display("%0dns\t %d  %d  %d  => %d  %d  %d", 
                  $time, a_in, b_in, c_in, a_out, b_out, c_out);

        $finish;
    end

endmodule
   
```
## Non Blocking:
```

module swap_three (
    input clk,
    input [7:0] a_in,
    input [7:0] b_in,
    input [7:0] c_in,
    output reg [7:0] a_out,
    output reg [7:0] b_out,
    output reg [7:0] c_out
);

always @(posedge clk) begin
    a_out <= b_in;
    b_out <= c_in;
    c_out <= a_in;
end

endmodule

//Testbench for non blocking

module swap_three_tb;

    // Inputs
    reg clk;
    reg [7:0] a_in;
    reg [7:0] b_in;
    reg [7:0] c_in;

    // Outputs
    wire [7:0] a_out;
    wire [7:0] b_out;
    wire [7:0] c_out;

    // Instantiate the Unit Under Test (UUT)
    swap_three uut (
        .clk(clk),
        .a_in(a_in),
        .b_in(b_in),
        .c_in(c_in),
        .a_out(a_out),
        .b_out(b_out),
        .c_out(c_out)
    );

    // Clock generation
    initial begin
        clk = 0;
        forever #5 clk = ~clk;  // 10ns clock period
    end

    // Test sequence
    initial begin
        // Display header
        $display("Time\t a_in b_in c_in => a_out b_out c_out");

        // Test case 1
        a_in = 8'd10;
        b_in = 8'd20;
        c_in = 8'd30;
        @(posedge clk);
        #1;
        $display("%0dns\t %3d  %3d  %3d => %3d   %3d   %3d", 
                 $time, a_in, b_in, c_in, a_out, b_out, c_out);

        // Test case 2
        a_in = 8'd5;
        b_in = 8'd15;
        c_in = 8'd25;
        @(posedge clk);
        #1;
        $display("%0dns\t %3d  %3d  %3d => %3d   %3d   %3d", 
                 $time, a_in, b_in, c_in, a_out, b_out, c_out);

        // Test case 3
        a_in = 8'd100;
        b_in = 8'd200;
        c_in = 8'd255;
        @(posedge clk);
        #1;
        $display("%0dns\t %3d  %3d  %3d => %3d   %3d   %3d", 
                 $time, a_in, b_in, c_in, a_out, b_out, c_out);

        $finish;
    end

endmodule
```
## output
## Blocking:
![Screenshot 2025-04-12 135447](https://github.com/user-attachments/assets/c1cbe5f9-a436-48c0-befd-1c6cca2853b2)



## NonBlocking:
![Screenshot 2025-04-12 135546](https://github.com/user-attachments/assets/c6b66085-d332-4d33-a3f4-3d273e4a92ba)

## Conclusion
In this experiment, a Verilog HDL code for swapping three numbers was designed and successfully simulated. The testbench verified the swapping operation, showing that the values of three input numbers (a, b, and c) were swapped correctly without the use of temporary variables. This experiment demonstrated the effectiveness of Verilog in implementing logical operations and control mechanisms such as swapping values. The simulation results confirm the correct functionality of the design.
