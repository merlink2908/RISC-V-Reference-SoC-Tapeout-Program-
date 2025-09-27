# GOOD MUX

## Verilog code

module good_mux (input i0, input i1, input sel, output reg y);

always @ (*)

begin

    if(sel)

        y <= i1;

    else 

        y <= i0;

end

endmodule

## Commands

iverilog good_mux.v tb_good_mux.v

./a.out

gtkwave tb_good_mux.vcd

![Setup Screenshot](1.png)

## Yosys Commands For Synthesis

yosys

read_liberty -lib /address/to/your/sky130/file/sky130_fd_sc_hd__tt_025C_1v80.lib

read_verilog good_mux.v

synth -top good_mux

abc -liberty /address/to/your/sky130/file/sky130_fd_sc_hd__tt_025C_1v80.lib

show

![Setup Screenshot](2.png)
