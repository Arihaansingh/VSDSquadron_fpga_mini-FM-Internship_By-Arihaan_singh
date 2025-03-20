# VSDSquadron_fpga_mini-FM-Internship_By-Arihaan_singh
The VSDSquadron FPGA Mini (FM) is a compact and low-cost development board designed for FPGA prototyping and embedded system projects. This board provides a seamless hardware development experience with an integrated programmer, versatile GPIO access, and onboard memory, making it ideal for students, hobbyists, and developers exploring FPGA-based designs. [(Source)](https://www.vlsisystemdesign.com/vsdsquadronfm/)
## Task 1 Understanding and Implementing the Verilog Code on the VSDSquadron FPGA Mini Board
### Step 1: Understanding the Verilog code
The Verilog code can be accessed from here [Verilog code](https://github.com/Arihaansingh/VSDSquadron_fpga_mini-FM-Internship_By-Arihaan_singh/blob/main/VSDFM_top_module.v) This Verilog module controls an RGB LED using an internal oscillator and a counter, with a test signal for monitoring and predefined brightness settings for the LEDs.

<details>
  <summary><STRONG> Verilog module overview</STRONG></summary>

### Port Analysis:

```verilog
module top (
    // outputs
    output wire led_red,   // Red
    output wire led_blue,  // Blue
    output wire led_green, // Green
    input wire hw_clk,     // Hardware Oscillator, not the internal oscillator
    output wire testwire
);
```
**This is the first part of the code which tells about the ports:**

`led_red`, `led_blue`, `led_green` **(Outputs):** These ports are intended to control the red, blue, and green components of an RGB LED, respectively. By driving these outputs high or low, the module can manipulate the color and intensity of the LED.

`hw_clk` **(Input):** This is the hardware oscillator clock input. Although the module utilizes an internal oscillator `(int_osc)` for its operations, it has the clock signal which drives the module signals.

`testwire` **(Output):** This port is connected to the 5 bit of the `frequency_counter_i` register `(frequency_counter_i[5])`. It serves as a test signal, potentially useful for debugging or monitoring the internal state of the frequency counter.

### Internal Component Analysis
The module consists of three main internal components, each serving a distinct function:

#### 1. Internal Oscillator (SB_HFOSC)
The internal oscillator generates a stable clock signal required for timing operations. It is configured with a clock division value of `0b10`, which corresponds to binary 2.

**Power and Enable Signals:**

`CLKHFPU = 1'b1`: Powers up the oscillator.
`CLKHFEN = 1'b1`: Enables the oscillator.

**Output Signal:**

`CLKHF`: This is the oscillator's output, connected to the internal signal `int_osc`, which drives the frequency counter and other timing-dependent operations.
#### 2. Frequency Counter Logic
This module includes a **28-bit counter**, named `frequency_counter_i`, which increments on every rising edge of `int_osc`.

**Functionality:**
- The counter continuously increases its value, providing a timing reference within the module.
- Bit 5 of this counter is specifically connected to `testwire`, allowing external monitoring of the frequency.
- This setup helps verify the oscillator's operation and timing accuracy.

#### 3. RGB LED Driver (SB_RGBA_DRV)
The module includes an RGB LED driver that controls the brightness and color of the LED.

**Configuration and Control:**

- `RGBLEDEN = 1'b1`: Enables the LED operation.
- `CURREN = 1'b1`: Enables current control for LED brightness.

**Color Output Settings:**

- **Red LED** (`RGB0`)**:** Set to minimum brightness (RGB0PWM = 1'b0).

- **Green LED** (`RGB1`)**:** Set to minimum brightness (RGB1PWM = 1'b0).

- **Blue LED** (`RGB2`)**:** Set to maximum brightness (RGB2PWM = 1'b1).

**Current Settings:**

- Each LED is configured with minimal current (`0b000001`) to optimize power consumption.

### Purpose 
This Verilog module is designed to control an RGB LED while also handling internal timing functions. It includes a stable built-in clock and ensures smooth LED operation. Additionally, it features a test signal that allows monitoring of system behavior. The module is ideal for embedded applications that require precise LED control without relying on external timing components.

### Description of internal logic and oscillator
The module generates its own clock signal using a **high-frequency oscillator** (`SB_HFOSC`). This oscillator serves as the timing source for the entire system. A **28-bit counter** is connected to the oscillator’s output, which helps keep track of time and internal processes.

To assist with debugging and monitoring, **bit 5** of this counter is linked to the `testwire` output. This connection allows external systems to observe and verify the clock’s operation.

### Functionality of the RGB LED driver and its relationship to the outputs
The **RGB LED driver** (`SB_RGBA_DRV`) is responsible for managing the brightness and color of the LED. It operates with the following settings:

- Uses a **current-controlled** output to regulate brightness efficiently.
- Each LED color (Red, Green, Blue) is controlled via **Pulse Width Modulation (PWM)**.
- **Predefined brightness levels:**
            - **Blue LED** is set to **maximum brightness** (`RGB2PWM = 1'b1`).
            - **Red and Green LEDs** are set to **minimum brightness** (`RGB0PWM = 1'b0`, `RGB1PWM = 1'b0`).

In short, **This Verilog module controls an RGB LED using an internal oscillator and a frequency counter while providing a test signal for monitoring.**
</details>

### Step 2: Creating the PCF File

The PCF (Physical Constraints File) can be acessed here [(PCF)](https://github.com/Arihaansingh/VSDSquadron_fpga_mini-FM-Internship_By-Arihaan_singh/blob/main/VsdFpgaMini.pcf). A PCF (Physical Constraints File) is used in FPGA design to define the mapping between logical signals in the HDL design and the physical pins of the FPGA device. It ensures that specific signals, such as clock inputs, LED outputs, or communication interfaces, are correctly assigned to the appropriate hardware pins. The PCF file consists of simple constraints using the `set_io1` command, associating signal names with pin numbers. This file plays a crucial role in ensuring proper hardware functionality, as incorrect assignments can lead to design failures or unexpected behavior

<details>
  <summary><STRONG> PCF analysis</STRONG></summary>
We can easily create a Physical Constraints File (PCF). We can create the Physical Constraints File (PCF) for the FPGA project using the 
  
[Datasheet](https://github.com/Arihaansingh/VSDSquadron_fpga_mini-FM-Internship_By-Arihaan_singh/blob/main/VSDSquadronFMDatasheet.pdf) Here's how:
  
1. Identify I/O Ports in Your Verilog Module: Examine your Verilog code to list all input and output ports that need to be mapped to physical pins.

2. Consult the VSDSquadronFM Datasheet: The datasheet provides detailed information about the board's pinout and functionalities. Locate the section detailing the FPGA's pin assignments to understand which physical pins correspond to specific functions.
   ![image](https://github.com/user-attachments/assets/47e8710a-fb94-42d5-94e4-c63b50327710)
See this image of the Datasheet which tells about the pin assignments

4. Create the PCF File: Using the information from the datasheet, map each Verilog I/O port to the appropriate physical pin. For example, if your Verilog module has an output led_red and the datasheet indicates that the red LED is connected to pin 39, your PCF entry would be:
```
set_io  led_red	39
```
So for this project we have created the [(PCF)](https://github.com/Arihaansingh/VSDSquadron_fpga_mini-FM-Internship_By-Arihaan_singh/blob/main/VsdFpgaMini.pcf).

![image](https://github.com/user-attachments/assets/6ec66888-4189-416a-a14e-0b1065d70a05)

#### More detailed explanation of each set_io command in your Physical Constraints File (PCF):

##### Understanding set_io Commands in PCF

The set_io command is used in FPGA development to map logical signals (used in HDL code) to specific physical pins on the FPGA. This ensures that inputs and outputs in your Verilog/VHDL code are correctly connected to the corresponding hardware pins.

##### Breakdown of Each set_io Command
1. `set_io led_red 39`
**Purpose:** This command assigns the logical signal `led_red` to pin 39 on the FPGA.
**Functionality:** When your HDL code sets `led_red` to HIGH (1), it will turn on the red LED connected to pin 39. Similarly, setting it to LOW (0) will turn it off.
Use Case: Typically used for LED status indicators (e.g., power, error, activity).

2. `set_io led_blue 40`
**Purpose:**  Maps the `led_blue` signal to pin 40.
**Functionality:** This allows the FPGA to control a blue LED, which will turn on/off based on the signal from the Verilog/VHDL code.
Use Case: Used for visual indicators, such as showing different states of the system.

3. `set_io led_green 41`
**Purpose:** Assigns the `led_green` signal to pin 41.
**Functionality:** The FPGA can now control a green LED, switching it on or off as needed.
Use Case: Often used for status LEDs, such as indicating successful operation.

4. `set_io hw_clk 20`
**Purpose:** Maps `hw_clk` (hardware clock signal) to pin 20.
**Functionality:** This allows the FPGA to receive clock inputs through pin 20, which are essential for timing operations inside the FPGA.
Use Case: Used for timing-sensitive applications, such as counters, PWM signals, or high-speed data processing.

5. `set_io testwire 17`
**Purpose:** Assigns `testwire` to pin 17.
**Functionality:** This is generally used for debugging or testing, allowing a test signal to be monitored or controlled externally.
Use Case: Can be used for temporary signal monitoring, debugging FPGA behavior, or testing different pin configurations.

##### Summary
Each `set_io` command plays a crucial role in defining FPGA pin assignments. Properly mapping logical signals to physical pins ensures correct functionality of the design and prevents errors in hardware interaction. These assignments are especially important when dealing with LEDs, clocks, and debugging signals, as they directly impact how the FPGA interacts with external components.
</details>
