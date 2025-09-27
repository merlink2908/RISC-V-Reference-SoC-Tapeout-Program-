# GLS

## Ternary Operator MUX

module ternary_operator_mux (input i0, input i1, input sel, output y);

  assign y = sel ? i1 : i0;
  
endmodule

iverilog -v ../my_lib/verilog_model/primitives.v -v ../my_lib/verilog_model/sky130_fd_sc_hd.v ternary_operator_mux_net.v tb_ternary_operator_mux.v    - Use this command followed by ./a.out to view the generated GLS VCD in gtkwave

![Setup Screenshot](4ternarymux.PNG)

![Setup Screenshot](4mux.PNG)

![Setup Screenshot](4glsmux.PNG)

## Bad MUX

module bad_mux (input i0, input i1, input sel, output reg y);

  always @ (sel) begin
  
    if (sel)
    
      y <= i1;
      
    else 
    
      y <= i0;
      
  end
  
endmodule

![Setup Screenshot](4badmux.PNG)

![Setup Screenshot](4badmuxglsmismatch.PNG)



##  Blocking Assignment Caveat

module blocking_caveat (input a, input b, input c, output reg d);

  reg x;
  
  always @ (*) begin
  
    d = x & c;
    
    x = a | b;
    
  end
  
endmodule

![Setup Screenshot](4blockingcaveat.PNG)

![Setup Screenshot](4blockingcaveatyosys.PNG)
![Setup Screenshot](4blockingcaveatglsmismatch.PNG)
