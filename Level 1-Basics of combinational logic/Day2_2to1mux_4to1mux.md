# Day2 - 2:1 mux and 4:1 mux

## Description
Designed and simulated verilog module for 2:1 mux and 4:1 mux using same testbench

---

## Design Code
```verilog
module mux_2(output y, input s,a,b);
    assign y = (s==0)?a:b;
endmodule

module mux_4(output reg [1:0] y, input s1,s2, input [1:0] a,b,c,d);
    always @(*) begin
        case ({s1, s2})
            2'b00: y = a;
            2'b01: y = b;
            2'b10: y = c;
            2'b11: y = d;
        endcase
    end
endmodule
```
## Testbench Code
```verilog
module mux_tb;
    reg [1:0] a,b,c,d;
    reg m,n,s,s1,s2;
    wire y1;
    wire [1:0] y2;

    mux_2 dut1(y1,s,m,n);
    mux_4 dut2(y2,s1,s2,a,b,c,d);

    initial begin
        $dumpfile("mux.vcd");
        $dumpvars;

        a=0; b=1; c=2; d=3; m=0; n=1;
        s=0; s1=0; s2=0;

        #10 s1=0; s2=1;
        #10 s1=1; s2=0; s=1;
        #10 s1=1; s2=1;
        #10 $finish;
    end
endmodule

