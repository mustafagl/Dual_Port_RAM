# Dual_Port_RAM
## Verilog File
```
module dual_port_ram 
  # (parameter ADDR_WIDTH = 4,
     parameter DATA_WIDTH = 16,
     parameter DEPTH = 16 
    )
  
  ( 	input 					clk,
   		input [ADDR_WIDTH-1:0]	addr,
   		inout [DATA_WIDTH-1:0]	data,
   		input 					cs,
   		input 					we,
   		input 					oe
  );
  
  reg [DATA_WIDTH-1:0] 	tmp_data;
  reg [DATA_WIDTH-1:0] 	mem [DEPTH:0];
  
  always @ (posedge clk) begin
    if (cs & we)
      mem[addr] <= data; // yazma
  end
  
  always @ (negedge clk) begin
    if (cs)
    	tmp_data <= mem[addr];
  end
  
  assign data = cs & oe ? tmp_data : 'hz; // okuma
endmodule

```
