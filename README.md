Task:

Design a circuit for receiving data words over an asynchronous serial line (UART_RX).

• Base your design on fundamental information about the operation and processing of asynchronous serial communication.

• Consider an input data stream in a fixed format: one START bit, 8 data bits, one STOP bit, transmitted at a rate of 9600 bauds per second. The receiving circuit will operate at a frequency 16 times higher (signal CLK) compared to the transmission rate of individual data bits. Your task will be to sample the data bits in the middle of the transmitted interval.

• The UART_RX circuit will receive individual bits at the input data port DIN, perform their de-serialization, and write the resulting 8-bit word to the data port DOUT. Confirm the validity of the data word on the DOUT port by setting the DOUT_VLD flag to a logic level of 1 for one clock cycle of the CLK signal.

<h2> Showcase from my documentation: </h2>

![image](https://github.com/AdamLnenicka/vhdl/assets/70570107/5259fd65-c804-48c0-b337-8d717ad559e2)

![image](https://github.com/AdamLnenicka/vhdl/assets/70570107/b2c34e6a-8785-4748-8691-39b70f9ba27a)

UART_RX Finite State Machine (UART_RX_FSM):

- **Purpose**: The UART_RX_FSM entity represents a finite state machine responsible for controlling the receiving (RX) side of a UART (Universal Asynchronous Receiver Transmitter) communication system. It processes incoming data bits and validates received data words.
  
- **Inputs**:
  - CLK: Clock signal for synchronization.
  - RST: Reset signal for resetting the state machine.
  - DIN: Data input representing the received data bit.
  - BIT_CNT: 4-bit vector representing the count of received data bits.
  - CLK_CNT: 4-bit vector representing the count of clock cycles.

- **Outputs**:
  - READ_EN: Read enable signal for controlling the reading process.
  - CLK_CNT_RSRT: Clock count reset signal.
  - VALID: Validity flag indicating the validity of the received data word.

- **States**:
  - WAIT_FOR_START: Waiting for the start bit.
  - WAIT_FOR_MID_BIT: Waiting for the middle of the start bit.
  - CLK_CNT_RST: Restarting the clock counter.
  - READING_DATA: Reading the data bits.
  - WAIT_FOR_STOP: Waiting for the stop bit.
  - VALIDATING: Validating the received data word.

- **Operation**:
  - The state machine transitions through different states based on the received input signals.
  - It waits for the start bit, detects the middle of the start bit, reads the data bits, and validates the received data word.

UART_RX (UART Receiver):

- **Purpose**: The UART_RX entity represents the receiver side of a UART communication system. It receives serial data, processes it using the UART_RX_FSM finite state machine, and outputs the received data word along with its validity flag.

- **Inputs**:
  - CLK: Clock signal for synchronization.
  - RST: Reset signal for resetting the receiver.
  - DIN: Data input representing the received data bit.

- **Outputs**:
  - DOUT: 8-bit vector representing the received data word.
  - DOUT_VLD: Validity flag indicating the validity of the received data word.

- **Operation**:
  - The receiver processes incoming data using the UART_RX_FSM.
  - It samples the incoming bits and validates the received data word.
  - The received data word is output along with its validity flag.

These components together provide the functionality of receiving and validating data words over an asynchronous serial communication line. The UART_RX entity incorporates the UART_RX_FSM to handle the receiving process efficiently and accurately.
