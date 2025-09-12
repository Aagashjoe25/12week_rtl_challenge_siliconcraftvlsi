# Day3 - 1:2, 1:4 mux and 1:8 demux

## Description
Designed and simulated verilog module for 1:2, 1:4 and 1:8 demux using same testbench

---

## Design Code
```verilog
module demux_2(output y1,y2, input x,sel);
   assign y1= (sel==0)?x:0;
   assign y2= (sel==1)?x:0;
endmodule

module demux_4(output reg [3:0] y, input x,input [1:0] sel);
    always @(*) begin
         y=4'b0000;
         y[sel]=x;
    end 
endmodule

module demux_8(output reg [7:0] y, input x,input [2:0] sel);
    always @(*) begin
        y= 8'b00000000;
        case(sel)
            3'b 000: y[0]=x;
            3'b 001: y[1]=x;
            3'b 010: y[2]=x;
            3'b 011: y[3]=x;
            3'b 100: y[4]=x;
            3'b 101: y[5]=x;
            3'b 110: y[6]=x;
            3'b 111: y[7]=x;
        endcase
    end 
endmodule
```
## Testbench Code
```verilog
module tb; 
    wire [1:0] ya; 
    wire [3:0] yb; 
    wire [7:0] yc; 

    reg  x,sela;
    reg [1:0] selb;
    reg [2:0] selc;

    demux_2 dut(ya[0],ya[1],x,sela);
    demux_4 du (yb,x,selb);
    demux_8 d  (yc,x,selc);

    initial begin
        $dumpfile("demux.vcd");
        $dumpvars;

        x=1;
        sela=0; selb= 2'b00; selc= 3'b000;
        #10 selc=3'b001;
        #10 selc=3'b010; selb=2'b01;
        #10 selc=3'b011; 
        #10 selc=3'b100; selb=2'b10; sela=1;
        #10 selc=3'b101;
        #10 selc=3'b110; selb=2'b11;
        #10 selc=3'b111;  
        #10 $finish;
    end 
endmodule
