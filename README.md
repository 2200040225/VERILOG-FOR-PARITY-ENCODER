Design code:

module parityencoder42(
    input [3:0] in,  
    output reg [1:0] out, 
    output reg parity 
);

    always @(*) begin
        case (in)
            4'b0001: out = 2'b00;  
            4'b0010: out = 2'b01;  
            4'b0100: out = 2'b10;  
            4'b1000: out = 2'b11;  
            default: out = 2'b00;  
        endcase
        parity = ^in; 
    end
endmodule

Test bench:

module parityencoder42_tb();
    reg [3:0] in; 
    wire [1:0] out;
    wire parity; 
    parity_encoder_4to2 uut (
        .in(in),
        .out(out),
        .parity(parity)
    );
    initial begin
        $monitor("Input = %b, Encoded Output = %b, Parity = %b", in, out, parity);
        in = 4'b0001;  
        #10;
        in = 4'b0010; 
        #10;
        in = 4'b0100;  
        #10;
        in = 4'b1000;  
        #10;
        in = 4'b1111;  
        #10;
        in = 4'b0000;  
        #10;
        $finish();
    end
endmodule
