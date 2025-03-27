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
    <details>
     <summary><STRONG> Block diagram illustrating the UART loopback architecture</STRONG></summary>
![image](https://github.com/user-attachments/assets/36fe2f6a-95c5-4d34-b74c-1568dbffcdf5)
  </details>
  <details>
     <summary><STRONG> Detailed circuit diagram showing connections between the FPGA and any peripheral devices used</STRONG></summary> 
    
![image](https://github.com/user-attachments/assets/eaff15eb-6a90-42c3-a44e-727a38fbbf84)
  </details>
  </details>

 ## Step 3 Implementation
  <details>
       <summary><STRONG> Transmitting code to FPGA Board</STRONG></summary>
    
### 🚀 UART Loopback on VSDSquadron FPGA

**📁 Setting Up the Project**

1. Create the following files inside a new folder under VSDSquadron_FM. In this case, the folder is named uart_loopback:

📜 Files to Create:

- 🛠️ Makefile
- 💾 uart_trx- Verilog
- 🏗️ Verilog file
- 📌 pcf (Pin Constraint File)
- 📌top module

📌 Folder Structure:

```
VSDSquadron_FM/
 ├── uart_loopback/
 │   ├── Makefile
 │   ├── uart_trx.v
 │   ├── top.v
 │   ├── uart_loopback.pcf
```

### 🔌 Connecting the FPGA Board

1️⃣ Plug in the FPGA Board to your system via USB-C.

2️⃣ Verify the Connection by running:

```
lsusb
```

💡 If the board is detected, you should see:

```
Future Technology Devices International
```

### 🛠️ Building & Flashing the Code

🔹 Navigate to the Folder

```
cd VSDSquadron_FM/uart_loopback
```

🔹 Build the Design

```
make build
```

🔹 Flash the FPGA Board (Run with sudo)

```
sudo make flash
```


✔️ Congratulations! You have successfully programmed your VSDSquadron FPGA for UART loopback testing! 🚀
  </details>

 ## Step 4 Testing and Verification
  <details>
       <summary><STRONG> Testing and Verification</STRONG></summary>

### 🖥️ Setting Up Docklight for UART Loopback Testing

**📥 Download & Install Docklight**

To test the UART loopback, we will be using Docklight, a serial communication software. You can download it from the [Docklight website](https://docklight.de/downloads/)
***
**🔌 Connecting & Configuring Docklight**

1️⃣ Open Docklight

2️⃣ Verify the Communication Port

**Ensure your system (not the VM) is connected to the correct COM port.*

**Default is COM1, but in my case, it was COM7.*

**If incorrect, change it by navigating to:*

```
Tools > Project Settings
```

3️⃣ Set the Baud Rate

**Speed: 9600**
***
**✉️ Sending & Receiving Data**

**🔹 Create a Send Sequence:**

1️⃣ Double-click on the small blue box under the "Name" column in the Send Sequences panel.

2️⃣ Enter the following details:

- 🏷️ Name: (Any descriptive label for your message)
- 🔣 Format: (Choose an appropriate data format)
- ✍️ Message: (Enter the message you want to send)

3️⃣ Click "Apply" and verify that your message appears under Send Sequences.

🔹 Transmit the Message:

1️⃣ Click the ➡️ (arrow) beside the name to send the message.

2️⃣ Verify the Response in the Receive Window.

**✅ If successful, the received message should match the sent message!**
***
✔️ Congratulations! You have successfully programmed your VSDSquadron FPGA for UART loopback testing! 🚀
</details>

## Step 3 Final Documentation
    
<details>      
    <summary><STRONG>Block and Circuit diagram</STRONG></summary>
<details>
     <summary><STRONG> Block diagram illustrating the UART loopback architecture</STRONG></summary
                                                                                           
![image](https://github.com/user-attachments/assets/36fe2f6a-95c5-4d34-b74c-1568dbffcdf5)
  </details>
  <details>
     <summary><STRONG> Detailed circuit diagram showing connections between the FPGA and any peripheral devices used</STRONG></summary> 
    
![image](https://github.com/user-attachments/assets/eaff15eb-6a90-42c3-a44e-727a38fbbf84)
  </details>
  </details>
