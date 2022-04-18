# JK-FLIPFLOP
JK flipflop in Verilog HDL
// Code your design here
module jk_ff(j,k,clk,rst,q,qbar);
  input j,k,clk,rst;
  output reg q,qbar;
  
  always @ (posedge clk)
    begin
      q=1;
      
      if (rst==0)
        begin
assign q= (~q & j) | (~k & q);
          qbar=~q;
         end
    end
      endmodule

// Code your testbench here
// or browse Examples
module jkff_test();
  reg j,k,clk,rst;
  wire q,qbar;
  
  //Instantiation
  jk_ff dut(j,k,clk,rst,q,qbar);
  
  initial
    begin
    clk=1'b0;
    forever #10 clk=~clk;
  end
  
  initial 
    begin
    j=1;k=0;rst=0;
    #100 j=0;k=1;
    #100 j=1;k=0;
    #100 j=1;k=1;
  end
  
  initial
    begin
    $monitor("At time=%t, clk=%b,rst=%b, j=%b,k=%b, q=%b,qbar=%b",$time,clk,rst,j,k,q,qbar);
      $dumpfile("jk_ff.vcd");
      $dumpvars(0,jkff_test);
    #500 $finish;
  end
endmodule


 
