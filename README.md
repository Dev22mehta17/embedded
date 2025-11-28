# embedded
and--
module and_gate_1;  
reg a, b; 
wire z; 
and my_and(z, a, b); 
always @(a or b) begin
$display("a= %b b= %b z= %b", a, b, z); 
end
initial begin 
a =0; b =0;
#10
a =0; b =1;
#10
a =1; b =0;
#10
a =1; b =1;
end 
endmodule

or--
module or_gate_1; 
reg a, b;
wire z;
or my_or(z, a, b);
3
always @(a or b) begin
$display("a= %b b= %b z= %b", a, b, z); 
end
initial begin 
a =0; b =0;
#10
a =0; b =1;
#10
a =1; b =0;
#10
a =1; b =1;
end 
endmodule

not--
module not_gate_1; 
reg a;
wire z;
assign z = ~a; 
always @(a) begin
$display("a= %b z= %b", a, z); 
end
initial begin 
a =0;
#10
a =1;
end 
endmodule

nand--
module nand_gate_1; 
reg a, b;
wire z;
nand my_nand(z, a, b); 
always @(a or b) begin
$display("a= %b b= %b z= %b", a, b, z); 
end
6
initial begin 
a =0; b =0;
#10
a =0; b =1;
#10
a =1; b =0;
#10
a =1; b =1;
end 
endmodule

nor--
module nor_gate_1; 
reg a, b;
wire z;
nor my_nor(z, a, b); 
always @(a or b) begin
$display("a= %b b= %b z= %b", a, b, z); 
end
initial begin 
a =0; b =0;
#10
a =0; b =1;
#10
a =1; b =0;
#10
a =1; b =1;
end 
endmodule

xor--
module xor_gate_1; 
reg a, b;
9
wire z;
xor my_xor(z, a, b); 
always @(a or b) begin
$display("a= %b b= %b z= %b", a, b, z); 
end
initial begin 
a =0; b =0;
#10
a =0; b =1;
#10
a =1; b =0;
#10
a =1; b =1;
end 
endmodule

xnor--
module xnor_gate_1; 
reg a, b;
wire z;
xnor my_xnor(z, a, b); 
always @(a or b) begin
$display("a= %b b= %b z= %b", a, b, z); 
end
initial begin 
a =0; b =0;
#10
a =0; b =1;
#10
a =1; b =0;
#10
a =1; b =1;
end 
endmodule

half adder-
module halfadder(a, b, sum, carry); 
input a, b;
output sum, carry;
assign sum = a ^ b; // Sum bit 
assign carry = a & b; // Carry bit 
endmodule
module halfadder_tb; 
reg a, b;
wire sum, carry;
halfadder add1(a, b, sum, carry); 
initial begin
$display("A\tB\tSum\tCarry");
$monitor("%b\t%b\t%b\t%b\n", a, b, sum, carry); 
a =0; b =0;
#1
13
a =0; b =1;
#1
a =1; b =0;
#1
a =1; b =1;
end 
endmodule

full adder-
module fulladder(a, b, c, sum, carry); 
input a, b, c;
output sum, carry; 
wire sum, carry; 
assign sum = a ^ b ^ c;
assign carry = ((a & b) | (b & c) | (a & c)); 
endmodule
module main; 
reg a, b, c;
wire sum, carry;
16
fulladder add(a, b, c, sum, carry); 
initial begin
$dumpfile("add.vcd");
$dumpvars(0, add);
$display("A\tB\tC\tSum\tCarry");
$monitor("%b\t%b\t%b\t%b\t%b\n", a, b,c, sum, carry); 
a =0; b =0; c =0;
#5
a =0; b =0; c =1;
#5
a =0; b =1; c =0;
#5
a =0; b =1; c =1;
#5
a =1; b =0; c =0;
#5
a =1; b =0; c =1;
#5
a =1; b =1; c =0;
#5
a =1; b =1; c =1;
end 
endmodule

half subtractor--
module half_sub(input a, b, output D, B); 
assign D = a ^ b;
assign B = ~a & b; 
endmodule
module half_sub_tb; 
reg a, b;
wire D, B;
half_sub hs(a, b, D, B); 
initial begin
$display("A\tB\tDifference\tBorrow");
$monitor("%b\t%b\t\t%b\t\t%b\n", a, b,D,B); 
a =0; b =0;
20
#1;
a =0; b =1;
#1;
a =1; b =0;
#1;
a =1; b =1;
end 
endmodule

bcd to exces3--
module BCD2Ex3(A, B, C, D, W, X, Y, Z);
input A, B, C, D; 
output W, X, Y, Z;
assign W = A | (B & C) | (B & D);
assign X = (~B & C) | (~B & D) | (B & ~C & ~D); 
assign Y = ~(C ^ D);
assign Z = ~D; 
endmodule
23
module test;
wire W, X, Y, Z;
reg A, B, C, D;
BCD2Ex3 object(A, B, C, D, W, X, Y, Z);
initial begin
$dumpfile("bcd.vcd");
$dumpvars(0, test);
$display(" A B C D | W X Y Z");
$monitor(" ", A, " ", B, " ", C, " ", D, " | ", W, " ", X, " ", Y, " ", Z); 
A =0; B=0; C=0;D=0;
#5 A=0;B=0;C=0;D=0;
#5 A=0;B=0;C=0;D=1;
#5 A=0;B=0;C=1;D=0;
#5 A=0;B=0;C=1;D=1;
#5 A=0;B=1;C=0;D=0;
#5 A=0;B=1;C=0;D=1;
#5 A=0;B=1;C=1;D=0;
#5 A=0;B=1;C=1;D=1;
#5 A=1;B=0;C=0;D=0;
#5 A=1;B=0;C=0;D=1;
end 
endmodule

4:1 multiplexer--
module mux(s1, s2, a, b, c, d, y); 
input s1, s2, a, b, c, d;
output y;
assign y = ~s1 & ~s2 & a | ~s1 & s2 & b | s1 & ~s2 & c | s1 & s2 & d; 
endmodule
module test;
reg a, b, c, d, s1, s2; 
wire y;
mux obj(s1, s2, a, b, c, d, y); 
initial begin
//$dumpfile("mux.vcd");
//$dumpvars(0, test);
$display("S1\t S2\t A \t B \t C \t D | Y");
$monitor("%b \t %b \t %b \t %b \t %b \t %b | %b", s1, s2, a, b, c, d, y); 
a =0; b =0; c =0; d =0; s1 = 0; s2 = 0;
#5 a=0;b=0;c=0;d=0;s1=0; s2 = 0;
#5 a=0;b=0;c=0;d=1;s1=0; s2 = 1;
#5 a=0;b=0;c=1;d=0;s1=1; s2 = 0;
#5 a=0;b=0;c=1;d=1;s1=1; s2 = 1;
#5 a=0;b=1;c=0;d=0;s1=0; s2 = 0;
#5 a=0;b=1;c=0;d=1;s1=0; s2 = 1;
26
#5 a=0;b=1;c=1;d=0;s1=1; s2 = 0;
#5 a=0;b=1;c=1;d=1;s1=1; s2 = 0;
#5 a=1;b=0;c=0;d=0;s1=0; s2 = 1;
#5 a=1;b=0;c=0;d=1;s1=0; s2 = 0;
#5 $finish; 
end 
endmodule

1:4 demux--
module demux(s1,s0,a,b,c,d,e,i); 
input s1,s0,e,i;
output a,b,c,d;
assign a =i&e&~s1&~s0; 
assign b =i&e&~s1&s0; 
assign c =i&e&s1&~s0; 
assign d =i&e&s1&s0; 
endmodule
module test; 
reg s1, s0, e, i;
wire a, b, c, d;
demux obj(s1,s0,a,b,c,d,e,i); 
initial begin
$dumpfile("demux.vcd");
$dumpvars(0, test);
$display("e\ts1\ts0\td\tc\tb\ta");
$monitor("%b\t%b\t%b\t%b\t%b\t%b\t%b" ,e,s1,s0,d,c,b,a); 
i=1; e=0; s1=0; s0=0;
#10 i=1; e=1; s1=0; s0=0; 
#10 i=1; e=1; s1=0; s0=1; 
#10 i=1; e=1; s1=1; s0=0;
29
#10 i=1; e=1; s1=1; s0=1;
end 
endmodule

2:4 decoder--
module decoder(a, b, c, d, e, f, E); 
input a, b, E;
output c, d, e, f; 
assign c = E & a & b;
assign d = E & a & (~b); 
assign e = E & (~a) & b; 
assign f = E & (~a) & (~b); 
endmodule
module testbench; 
reg a, b, E;
wire c, d, e, f;
decoder obj(a, b, c, d, e, f, E); 
initial begin
$display("Inputs | Outputs");
$display("E a b | c d e f");
$monitor("%b %b %b | %b %b %b %b",E,a,b, c, d, e, f); 
E =0; a=0; b=0;
#5 E =1; a=0; b=0;
#5 E =1; a=0; b=1;
#5 E =1; a=1; b=0;
#5 E =1; a=1; b=1;
31
#5 $finish; 
end 
endmodule

4:2 encoder--
module encoder(a, b, c, d, p, q); 
input a, b, c, d;
output p, q; 
assign p = a | b; 
assign q = a | c; 
endmodule 
module test; 
reg a, b, c, d; 
wire p, q;
encoder obj(a, b, c, d, p, q); 
initial begin
$display("Inputs | Outputs");
$display("A B C D | P Q");
$monitor("%b %b %b %b | %b %b",a, b, c, d, p, q); 
a =0; b =0; c =0; d =1;
#5 a =0; b =0; c =1; d =0;
#5 a =0; b =1; c =0; d =0;
#5 a =1; b =0; c =0; d =0;
end 
endmodule

d flip flop--
module dff_from_nand(); 
wire Q,Q_BAR;
reg D,CLK;
nand U1 (X,D,CLK) ;
nand U2 (Y,X,CLK) ; 
nand U3 (Q,Q_BAR,X); 
nand U4 (Q_BAR,Q,Y);
initial begin
$monitor("CLK = %b D = %b Q = %b Q_BAR = %b",CLK, D, Q, Q_BAR); 
CLK = 0;
D = 0;
#3 D = 1;
#3 D = 0;
#3 $finish; 
end
always #2 CLK = ~CLK; 
endmodule

jk flip flop--
module jkff(input [1:0] jk,input clk,output q,output qb); 
reg q,qb;
always@(posedge clk) 
begin
case(jk) 
2'b00: q=q; 
2'b01: q=0;
2'b10: q=1;
2'b11: q=~q; 
endcase 
qb=~q;
end 
endmodule 
module test; 
reg [1:0]jk; 
reg clk,i; 
wire q,qb;
jkff ob(jk,clk,q,qb); 
initial begin
$dumpfile("first.vcd");
$dumpvars(1,test);
$display("clk\tjk1\tjk0\tq\t~q");
$monitor("%b\t%b\t%b\t%b\t%b",clk,jk[1],jk[0],q,qb); 
jk=2'b00;#10
jk=2'b01;#10 
jk=2'b10;#10 
jk=2'b11;#10
$finish; 
end
initial begin
clk=0; 
for(i=0;i<=20;i++) 
#5 clk=~clk;
end 
endmodule

asynchronous up--
module async_up_counter( 
input clk,
input rst,
output QA, QB, QC
);
reg [2:0] cnt;
assign QA = cnt[0]; 
assign QB = cnt[1]; 
assign QC = cnt[2];
always @(negedge clk or posedge rst) begin 
if (rst)
cnt <= 3'b000; 
else
cnt <= cnt + 1; 
end
endmodule
module test_async_up_counter; 
reg clk, rst;
wire QA, QB, QC; 
integer cycle_num;
async_up_counter uut (
.clk(clk),
.rst(rst),
.QA(QA),
.QB(QB),
.QC(QC)
);
initial begin 
clk = 0;
rst = 1;
cycle_num = 1;
#5 rst = 0;
$display("3-bit Asynchronous Up Counter");
$display("Cycle | QC QB QA");
$monitor(" %0d | %b %b %b", cycle_num, QC, QB, QA); 
repeat (8) begin
#5 clk = ~clk; 
#5 clk = ~clk;
cycle_num = cycle_num + 1; 
end
$finish; 
end 
endmodule

async down--
module async_down_counter( 
input clk,
input rst,
output QA, QB, QC
);
reg [2:0] cnt;
assign QA = cnt[0]; 
assign QB = cnt[1]; 
assign QC = cnt[2];
always @(negedge clk or posedge rst) begin 
if (rst)
cnt <= 3'b111; 
else
cnt <= cnt - 1; 
end
endmodule
module test_async_down_counter; 
reg clk, rst;
wire QA, QB, QC; 
integer cycle_num;
async_down_counter uut (
.clk(clk),
.rst(rst),
.QA(QA),
.QB(QB),
.QC(QC)
);
initial begin 
clk = 0;
rst = 1;
cycle_num= 1;
#5 rst = 0;
$display("3-bit Asynchronous Down Counter");
$display("Cycle | QC QB QA");
$monitor(" %0d | %b %b %b", cycle_num, QC, QB, QA); 
repeat (8) begin
#5 clk = ~clk; 
#5 clk = ~clk;
cycle_num = cycle_num + 1 
end
$finish; 
end 
endmodule
