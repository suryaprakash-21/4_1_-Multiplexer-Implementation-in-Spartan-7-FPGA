# 4_1_-Multiplexer-Implementation-in-Spartan-7-FPGA
# EXP NO: 1.B 4:1 Multiplexer Implementation in Spartan-7 FPGA
# Aim
To design, synthesize, and implement a 4:1 Multiplexer using Verilog HDL on a Spartan-7 FPGA using Xilinx Vivado Design Suite.

# Apparatus Required
| S.No | Column 2        | Column 3                              |
|------|-------          |----------                             |
|  1   | FPGA Board      | Xilinx Spartan-7 development board    |
|  2   | Software        | Xilinx Vivado Design Suite            |
|  3   | Cable           | USB Programming Cable (JTAG/USB-JTAG) |


# Theory
A 4:1 multiplexer selects one of four data inputs (i0..i3) and routes it to a single output y, based on two select lines sel[1:0].

# Truth table

| S1   | S0  | Y  |
|------|-----|----|
|  0   | 0   | D0 |
|  0   | 1   | D1 |
|  1   | 0   | D2 |
|  1   | 1   | D3 |

# Procedure (Vivado Design Suite)
Create Project

Open Vivado → Create New Project.
Name project MUX_4to1_Spartan7. Select RTL Project, enable Do not specify sources at this time (or add immediately).
Choose the correct Spartan-7 device/board for your hardware.
Create Design Source

Flow Navigator → Add Sources → Add or Create Design Sources.
Create file mux4to1.v and type the Verilog code.
Add Constraints

Add XDC file mux4to1.xdc and map inputs/outputs to board pins.
Synthesize & Implement
Run Synthesis → inspect warnings/errors.
Run Implementation → review timing and utilization.
Generate Bitstream & Program
Generate Bitstream.
Open Hardware Manager → connect to target → Program device with .bit file.
Verify outputs on LEDs/scope.

# Verilog Program (mux4to1.v)
```
module mux4to1 (
    input  wire [3:0] I,     // I[0], I[1], I[2], I[3]
    input  wire [1:0] sel,   // sel[0], sel[1]
    output reg  y
);

always @(*) begin
    case(sel)
        2'b00: y = I[0];
        2'b01: y = I[1];
        2'b10: y = I[2];
        2'b11: y = I[3];
        default: y = 1'b0;
    endcase
end
endmodule
```
# Constraint file for Seven-Segment Display
```
set_property -dict {PACKAGE_PIN V2 IOSTANDARD LVCMOS33} [get_ports {I[0]}]
set_property -dict {PACKAGE_PIN U2 IOSTANDARD LVCMOS33} [get_ports {I[1]}]
set_property -dict {PACKAGE_PIN U1 IOSTANDARD LVCMOS33} [get_ports {I[2]}]
set_property -dict {PACKAGE_PIN T2 IOSTANDARD LVCMOS33} [get_ports {I[3]}]
set_property -dict {PACKAGE_PIN K2 IOSTANDARD LVCMOS33} [get_ports {sel[0]}]
set_property -dict {PACKAGE_PIN K1 IOSTANDARD LVCMOS33} [get_ports {sel[1]}]
set_property -dict {PACKAGE_PIN G1 IOSTANDARD LVCMOS33} [get_ports {y}]
```
# FPGA Implementation Output

![4x1 mux](https://github.com/user-attachments/assets/26aa6934-474e-43f7-9b2b-49d4d11f18fe)

# Conclusion
The 4:1 multiplexer was successfully designed,synthesized, and implemented (bitstream generated) in the Spartan-7 FPGA. The output matches the expected truth table.
