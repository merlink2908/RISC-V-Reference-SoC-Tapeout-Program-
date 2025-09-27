# Optimisation

## 1) Verilog Code

module opt_check (input a , input b , output y);

	assign y = a?b:0;
  
endmodule

opt_clean -purge:Use it during synthesis to remove unused or redundant objects from the design

![Setup Screenshot](3optcheck.PNG)

## 2) Verilog Code

module opt_check2 (input a , input b , output y);

	assign y = a?1:b;
  
endmodule

![Setup Screenshot](3optcheckor.PNG)

## 3) Verilog Code

module opt_check2 (input a , input b , output y);

	assign y = a?1:b;
  
endmodule

![Setup Screenshot](3optcheck3and.PNG)

## 4) Verilog Code

module dff_const1(input clk, input reset, output reg q);

always @(posedge clk, posedge reset)

begin

	if(reset)
  
		q <= 1'b0;
    
	else
  
		q <= 1'b1;
end

endmodule

![Setup Screenshot](3dff1.PNG)

![Setup Screenshot](3dffconst1.PNG)

## 5) Verilog Code

module dff_const2(input clk, input reset, output reg q);

always @(posedge clk, posedge reset)

begin

	if(reset)
  
		q <= 1'b1;
    
	else
  
		q <= 1'b1;
    
end

endmodule

![Setup Screenshot](3dff2alwaya1.PNG)

![Setup Screenshot](3dffcont2.PNG)

## 6) Verilog Code

module dff_const3(input clk, input reset, output reg q);

reg q1;

always @(posedge clk, posedge reset)

begin

	if(reset)

	begin

		q <= 1'b1;

		q1 <= 1'b0;

	end

	else

	begin

		q1 <= 1'b1;

		q <= q1;

	end

end

endmodule

![Setup Screenshot](3dff3.PNG)

![Setup Screenshot](3dffconst3.PNG)
