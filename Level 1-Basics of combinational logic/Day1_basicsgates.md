# Day1 - logic gates

## Description
Designed and simulated verilog module for or, and, not, nand, nor, xor and xnor gates with testbench
using iverilog and gtkwave

---

## Design Code
```verilog
1   module gates(output and_out, or_out, not_out,
  1                     xor_out, xnor_out, nand_out, nor_out,
  2              input a,b);
  3 
  4     assign and_out= a&b;
  5     assign or_out= a|b;
  6     assign not_out= ~a;
  7     assign xor_out= a^b;
  8     assign xnor_out= a~^b;
  9     assign nand_out= a~&b;
 10     assign nor_out= a~|b;
 11 
 12 endmodule;
```
## Testbench Code
```verilog
module gates_tb;
  1     reg a,b;
  2     wire and_out,or_out,not_out,xor_out,xnor_out,nand_out,nor_out;
  3 
  4     gates dut(and_out,or_out,not_out,xor_out,xnor_out,nand_out,nor_out,a,b);
  5 
  6     initial begin
  7         $dumpfile("gates.vcd");
  8         $dumpvars;
  9 
 10         a=0; b=0; #10;
 11         a=0; b=1; #10;
 12         a=1; b=0; #10;
 13         a=1; b=1; #10;
 14         $finish;
 15     end
 16 endmodule;
