Task:

Design a circuit for receiving data words over an asynchronous serial line (UART_RX).

• Base your design on fundamental information about the operation and processing of asynchronous serial communication.

• Consider an input data stream in a fixed format: one START bit, 8 data bits, one STOP bit, transmitted at a rate of 9600 bauds per second. The receiving circuit will operate at a frequency 16 times higher (signal CLK) compared to the transmission rate of individual data bits. Your task will be to sample the data bits in the middle of the transmitted interval.

• The UART_RX circuit will receive individual bits at the input data port DIN, perform their de-serialization, and write the resulting 8-bit word to the data port DOUT. Confirm the validity of the data word on the DOUT port by setting the DOUT_VLD flag to a logic level of 1 for one clock cycle of the CLK signal.
