module vending_machine (
  input clk,
  input reset,
  input [3:0] coin,        
  input select,
  input refund,
  output reg dispense,
  output reg change,
  output reg invalid,
  output reg [3:0] led,    
  output reg [6:0] seg     
);
  reg [7:0] balance;
  always @(*) begin
    case (balance)
      0:  seg = 7'b1000000; //{a,b,c,d,e,f,g}
      1:  seg = 7'b1111001;
      2:  seg = 7'b0100100;
      3:  seg = 7'b0110000;
      4:  seg = 7'b0011001;
      5:  seg = 7'b0010010;
      6:  seg = 7'b0000010;
      7:  seg = 7'b1111000;
      8:  seg = 7'b0000000;
      9:  seg = 7'b0010000;
      10: seg = 7'b0001000;
      11: seg = 7'b0000011;
      12: seg = 7'b1000110;
      13: seg = 7'b0100001;
      14: seg = 7'b0000110;
      15: seg = 7'b0001110;
      default: seg = 7'b1111111;
    endcase
  end   
  always @(posedge clk or posedge reset) begin
    if (reset) begin
      balance<=0;
        dispense<=0;
      change <= 0;
      invalid <= 0;
      led <= 4'b0000;
    end else begin
      dispense <= 0;
      change <= 0;
      invalid <= 0;
      led <= 4'b0000;
      if (coin == 4'd5 || coin == 4'd10 || coin == 4'd15) begin
        balance <= balance + coin;
        led[0] <= 1; // Valid coin
      end else if (coin != 4'd0) begin
        invalid <= 1;
        led[2] <= 1; // Invalid coin
      end
      if (refund && balance > 0) begin
        balance <= 0;
        led[1] <= 1; // Refund 
      end
      if (select && balance >= 15) begin
        dispense <= 1;
        led[3] <= 1; // Dispense
        if (balance > 15)
          change <= 1;
        balance <= 0;
      end
    end
  end
endmodule
