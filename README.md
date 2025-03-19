# VSDSquadron_fpga_mini-FM-Internship_By-Arihaan_singh
The VSDSquadron FPGA Mini (FM) is a compact and low-cost development board designed for FPGA prototyping and embedded system projects. This board provides a seamless hardware development experience with an integrated programmer, versatile GPIO access, and onboard memory, making it ideal for students, hobbyists, and developers exploring FPGA-based designs. [(Source)](https://www.vlsisystemdesign.com/vsdsquadronfm/)
## Task 1
### Step 1: Understanding the Verilog code
**Review the module declaration and understand the purpose of each input and output port:**

`led_red`, `led_blue`, `led_green` **(Output):** Control the RGB LED

`hw_clk` **(Input):** Hardware oscillator clock input

`testwire` **(Output):** Test signal output

<details>
  <summary>▶ Module Analysis</summary>

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

#### Overview of the RGB LED Controller
This Verilog module is designed to control an RGB LED while also handling internal timing functions. It includes a stable built-in clock and ensures smooth LED operation. Additionally, it features a test signal that allows monitoring of system behavior. The module is ideal for embedded applications that require precise LED control without relying on external timing components.

#### Clock System and Timing Mechanism
The module generates its own clock signal using a **high-frequency oscillator** (`SB_HFOSC`). This oscillator serves as the timing source for the entire system. A **28-bit counter** is connected to the oscillator’s output, which helps keep track of time and internal processes.

To assist with debugging and monitoring, **bit 5** of this counter is linked to the `testwire` output. This connection allows external systems to observe and verify the clock’s operation.

#### RGB LED Control and Configuration
The RGB LED driver (SB_RGBA_DRV) is responsible for managing the brightness and color of the LED. It operates with the following settings:

Uses a current-controlled output to regulate brightness efficiently.
Each LED color (Red, Green, Blue) is controlled via Pulse Width Modulation (PWM).
Predefined brightness levels:
Blue LED is set to maximum brightness (RGB2PWM = 1'b1).
Red and Green LEDs are set to minimum brightness (RGB0PWM = 1'b0, RGB1PWM = 1'b0).
This setup ensures that the LED displays the correct color with stable and power-efficient performance.
