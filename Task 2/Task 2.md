# VSDSquadron_fpga_mini-FM-Internship_By-Arihaan_singh
The VSDSquadron FPGA Mini (FM) is a compact and low-cost development board designed for FPGA prototyping and embedded system projects. This board provides a seamless hardware development experience with an integrated programmer, versatile GPIO access, and onboard memory, making it ideal for students, hobbyists, and developers exploring FPGA-based designs. [(Source)](https://www.vlsisystemdesign.com/vsdsquadronfm/)
## Task 2 Implementing a UART loopback
### Step 1: Understanding the Verilog code
### UART Loopback Overview
**UART (Universal Asynchronous Receiver-Transmitter)** is a hardware communication protocol used for serial communication between devices. It operates using two primary data lines:

- **TX (Transmit) pin** – Sends data
- **RX (Receive) pin** – Receives data

A UART loopback mechanism is a test mode where transmitted data (TX) is directly fed back into the receive line (RX) of the same module. This allows verification of UART functionality without requiring an external device.

🔗 [View the existing code here](https://github.com/Arihaansingh/VSDSquadron_fpga_mini-FM-Internship_By-Arihaan_singh/blob/main/Task%202/uart_trx.v)

<details>
  <summary><STRONG> Verilog module overview</STRONG></summary>

### Analysis:

### 🚀 Module Breakdown
This module is designed to implement a UART loopback mechanism while also controlling an RGB LED based on the received data.

### ⚙️ Main Components
#### 🟢 Clock System

- Uses an Internal Oscillator (`SB_HFOSC`) to generate a clock signal.

- Configured with `CLKHF_DIV = "0b10"` to divide the frequency.

- Provides a timing reference for all operations.

#### 🔴 UART Loopback Communication

- TX (Transmit) and RX (Receive) pins are directly connected within the module.

- Any data sent to `uarttx` is immediately received at `uartrx`.

- This feature is useful for self-testing UART functionality without needing another device.

#### 🔵 Frequency Counter

- A 28-bit counter (`frequency_counter_i`) tracks oscillator cycles.

- It increases on each positive edge of the clock signal.

- Helps generate timing signals for internal operations.

#### 🟡 RGB LED Driver (SB_RGBA_DRV)

- Controls three LEDs: Red (`led_red`), Green (`led_green`), and Blue (`led_blue`).

- Uses PWM (Pulse Width Modulation) to adjust brightness levels.

- UART data is directly mapped to LED brightness, allowing for visual feedback.

### 🔁 How It Works
#### ✅ Receiving UART Data

- Data arrives at the `uartrx` pin.

- The same data is looped back to `uarttx` and sent out again.

- This confirms that UART transmission and reception are functioning correctly.

#### ✅ LED Control Based on UART Data

- The received data is used to control the intensity of the RGB LEDs.

- PWM signals regulate LED brightness based on input values.

- All three LEDs change intensity together based on UART input.

#### ✅ Clock & Timing Management

- The internal oscillator ensures stable timing.

- The frequency counter generates signals for PWM and UART operations.

  **This system efficiently tests UART communication while providing real-time LED feedback. 🌟**
  </details>
  
  ## Step 2 Design documentetion
    <details>
       <summary><STRONG> Analysis</STRONG></summary>
    </details>
    <details>
     <summary><STRONG> Block diagram illustrating the UART loopback architecture</STRONG></summary>
![image](https://github.com/user-attachments/assets/36fe2f6a-95c5-4d34-b74c-1568dbffcdf5)
  </details>
  <details>
     <summary><STRONG> Detailed circuit diagram showing connections between the FPGA and any peripheral devices used</STRONG></summary>
![image](https://github.com/user-attachments/assets/c12b02d6-1b4d-41a3-841e-328ac90cc7b9)
  </details>

