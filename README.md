# 4.SIMULATION AND IMPLEMENTATION OF SEQUENTIAL LOGIC CIRCUITS

# AIM: 
 To simulate and synthesis SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using VIVADO 2023.2

# APPARATUS REQUIRED:
VIVADO 2023.1

**LOGIC DIAGRAM**

SR FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/77fb7f38-5649-4778-a987-8468df9ea3c3)


JK FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/1510e030-4ddc-42b1-88ce-d00f6f0dc7e6)

T FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/7a020379-efb1-4104-85ee-439d660baa08)


D FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/dda843c5-f0a0-4b51-93a2-eaa4b7fa8aa0)


COUNTER

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/a1fc5f68-aafb-49a1-93d2-779529f525fa)


  
# PROCEDURE:
1. Open Vivado: Launch Xilinx Vivado software on your computer.
2. Create a New Project: Click on "Create Project" from the welcome page or navigate through
"File" > "Project" > "New".
3. Project Settings: Follow the prompts to set up your project. Specify the project name, location,
and select RTL project type.
4. Add Design Files: Add your Verilog design files to the project. You can do this by right-clicking
on "Design Sources" in the Sources window, then selecting "Add Sources". Choose your Verilog
files from the file browser.
5. Specify Simulation Settings: Go to "Simulation" > "Simulation Settings". Choose your
simulation language (Verilog in this case) and simulation tool (Vivado Simulator).
6. Run Simulation: Go to "Flow" > "Run Simulation" > "Run Behavioral Simulation". This will
launch the Vivado Simulator and compile your design for simulation.
7. Set Simulation Time: In the Vivado Simulator window, set the simulation time if it's not set
automatically. This determines how long the simulation will run.
8. Run Simulation: Start the simulation by clicking on the "Run" button in the simulation window.
9. View Results: After the simulation completes, you can view waveforms, debug signals, and
analyze the behavior of your design.

# D-FLIP FLOP:
# VERILOG CODE
module Dflipflop(D,clk,reset,Q);
input D;
input clk;
input reset;
output reg Q;
always @(posedge clk)
begin
if(reset==1'b1)
Q <= 1'b0;
else
Q <= D;
end
endmodule

# OUTPUT:
![image](https://github.com/sakthivelM24/VLSI-LAB-EXP-4/assets/165649785/44a91e81-27d5-4225-80ed-c4f8e6e95186)
![image](https://github.com/sakthivelM24/VLSI-LAB-EXP-4/assets/165649785/7ee1d3eb-fd6b-4975-8204-3067171fa581)

# JK FLIP FLOP:
# VERILOG CODE
module JK_flipflop (q, q_bar, j,k, clk,reset);
input j,k,clk, reset;
output reg q;
output q_bar;
always@(posedge clk)
begin
if(!reset)
q <= 0;
else
begin
case({j,k})
2'b00: q <= q; // No change
2'b01: q <= 1'b0; // reset
2'b10: q <= 1'b1; // set
2'b11: q <= ~q; // Toggle
endcase
end
end
assign q_bar = ~q;
endmodule

# OUTPUT:
![image](https://github.com/sakthivelM24/VLSI-LAB-EXP-4/assets/165649785/81816bcf-c7e4-4401-856d-0970ab9ae7fd)
![image](https://github.com/sakthivelM24/VLSI-LAB-EXP-4/assets/165649785/c7e53488-fb9b-4e6f-b8b5-f13af315764f)

# MOD-10 COUNTER
# VERILOG CODE
module mod10(clk,rst,out);
input clk,rst;
output reg [3:0]out;
always@(posedge clk)
begin
if (rst==1 | out==4'b1001)
out=4'b0000;
else
out=out+1;
end
endmodule

# OUTPUT:
![image](https://github.com/sakthivelM24/VLSI-LAB-EXP-4/assets/165649785/b67ab6b1-f9e0-4516-9c49-a522bdf9b430)
![image](https://github.com/sakthivelM24/VLSI-LAB-EXP-4/assets/165649785/59acb545-7e52-4a92-939a-8e83c7a14f09)

# RIPPLE CARRY COUNTER
# VERILOG CODE
module tff(q,clk,rst);
input clk,rst;
output q;
wire d;
dff df1(q,d,clk,rst);
not n1(d,q);
endmodule
module dff(q,d,clk,rst);
input d,clk,rst;
output q;
reg q;
always @(posedge clk or posedge rst)
begin
if (rst)
q=1'b0;
else
q=d;
end
endmodule
module ripplecounter(clk,rst,q);
input clk,rst;
output [3:0]q;
tff tf0(q[0],clk,rst);
tff tf1(q[1],q[0],rst);
tff tf2(q[2],q[1],rst);
tff tf3(q[3],q[2],rst);
endmodule

# OUTPUT:
![image](https://github.com/sakthivelM24/VLSI-LAB-EXP-4/assets/165649785/62affcdf-5eeb-46b4-af6e-106672b2a617)
![image](https://github.com/sakthivelM24/VLSI-LAB-EXP-4/assets/165649785/9571b375-f336-4dc6-a4ac-46ee8d6e9901)

# SR FLIP FLOP
# VERILOG CODE
module sr_flipflop(s,r,clk,rst,q);
input s,r,clk,rst;
output reg q;
always@(posedge clk)
begin
if(rst==1)
q=0;
else
begin
case({s,r})
2'b00:q=q;
2'b01:q=0;
2'b10:q=1;
2'b11:q=1'bX;
endcase
end
end
endmodule

# OUTPUT:
![image](https://github.com/sakthivelM24/VLSI-LAB-EXP-4/assets/165649785/65d71060-7467-4300-8123-3d4b84b16d34)
![image](https://github.com/sakthivelM24/VLSI-LAB-EXP-4/assets/165649785/08369c83-6549-4490-a18a-d7493501a4f4)

# T FLIP FLOP
# VERILOG CODE
module T_flipflop(clk,rst,t,q);
input clk,rst,t;
output reg q;
always @(posedge clk)
begin
if (rst==1)
q=1'b0;
else if (t==0)
q=q;
else
q=~q;
end
endmodule

# OUTPUT:
![image](https://github.com/sakthivelM24/VLSI-LAB-EXP-4/assets/165649785/194a6ffd-9a8b-4631-92ac-0779fdb58ead)
![image](https://github.com/sakthivelM24/VLSI-LAB-EXP-4/assets/165649785/b28f4268-6d2c-4b18-aaf7-a9c2c3f8a342)

# UP-DOWN COUNTER
# VERILOG CODE
module updown_counter(clk,rst,updown,out);
input clk,rst,updown;
output reg [3:0]out;
always@(posedge clk)
begin
if (rst==1)
out=4'b0000;
else if(updown==1)
out=out+1;
else
out=out-1;
end
endmodule

# OUTPUT:
![image](https://github.com/sakthivelM24/VLSI-LAB-EXP-4/assets/165649785/a0aa0773-dd12-4b9a-8bec-7e7c3e57732b)
![image](https://github.com/sakthivelM24/VLSI-LAB-EXP-4/assets/165649785/72c5b67b-a61c-491c-9e1b-87882da3ea6f)

# RESULT:
Hence The simulation and synthesis of SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using Vivado 2023
is done and output verified successfully.


