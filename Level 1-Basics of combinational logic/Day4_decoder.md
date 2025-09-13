# Day3 - 2:4, 3:8 mux and 4:16 decoder

## Description
Designed and simulated verilog module for 2:4, 3:8 mux and 4:16 decoder using same testbench with for loop

---

## Design Code
```verilog
module dec_2to4(output reg [3:0] out,input en,input [1:0] in);
    always@(*) begin
        if(en==1) begin
            case(in)
                2'b00: out= 4'b0001;
                2'b01: out= 4'b0010;
                2'b10: out= 4'b0100;
                2'b11: out= 4'b1000;
            endcase
        end
        else out= 4'b0000;
    end 
endmodule

module dec_3to8(output reg [7:0] out,input en,input [2:0] in);
    always@(*) begin
        out= 8'b0;
        if(en==1)
            out[in]=1;
    end 
endmodule

module dec_4to16(output [15:0] out,input en,input [3:0] in);
    assign out= (en==1)? 1<<in:16'b0;
endmodule
```
## Testbench Code
```verilog
module tb; 
    reg [1:0] ina;
    reg [2:0] inb;
    reg [3:0] inc;
    reg en; 

    wire [3:0] outa;
    wire [7:0] outb;
    wire [15:0] outc;

    dec_2to4 dut1(outa,en,ina);
    dec_3to8 dut2(outb,en,inb);
    dec_4to16 dut3(outc,en,inc);

    initial begin
        $dumpfile("decoder.vcd");
        $dumpvars;

        en=1; ina=2'b0; inb=3'b0; inc=4'b0; 
    
        for(integer i=1;i<=16;i+=1) begin
            #10 inc+=1;
            if(i%2==0) inb+=1;
            if(i%4==0) ina+=1;
        end
    end 
endmodule
