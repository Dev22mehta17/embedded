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
