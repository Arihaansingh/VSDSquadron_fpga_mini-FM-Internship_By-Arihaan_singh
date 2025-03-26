# Objective:
Participants are expected to understand and document the provided Verilog code, create the necessary PCF file, and integrate the design with the VSDSquadron FPGA Mini board using the provided datasheet. (install tools as explained in datasheet)

## Step 1: Understanding the Verilog Code

- Access the Verilog code from the provided link: https://github.com/thesourcerer8/VSDSquadron_FM/blob/main/led_blue/top.v

- Review the module declaration and understand the purpose of each input and output port:

```
led_red, led_blue, led_green (Output): Control the RGB LED

hw_clk (Input): Hardware oscillator clock input

testwire (Output): Test signal output
```

- Analyze the internal components:

- Internal Oscillator (`SB_HFOSC`) instantiation

- Frequency counter logic driven by the internal oscillator

- RGB LED driver instantiation with defined current parameters

- Create a brief documentation explaining the functionality of the Verilog code, including:

- Purpose of the module

- Description of internal logic and oscillator

- Functionality of the RGB LED driver and its relationship to the outputs

## Step 2: Creating the PCF File

- Access the PCF file from the provided link: https://github.com/thesourcerer8/VSDSquadron_FM/blob/main/led_blue/VSDSquadronFM.pcf

- Understand the pin assignments from the PCF file:
```
led_red -> Pin 39
led_blue -> Pin 40
led_green -> Pin 41
hw_clk -> Pin 20
testwire -> Pin 17
```
- Cross-reference the pin assignments with the VSDSquadron FPGA Mini board datasheet to verify the correctness of the assignments.

- Document the pin mapping and explain the significance of each connection in context with the Verilog code and board hardware.

## Step 3: Integrating with the VSDSquadron FPGA Mini Board

- Review the VSDSquadron FPGA Mini board datasheet to understand its features and pinout.

- Use the datasheet to correlate the physical board connections with the PCF file and Verilog code.

- Connect the board to the computer as described in the datasheet (e.g., using USB-C and ensuring FTDI connection).

- Follow the provided [Makefile](https://github.com/thesourcerer8/VSDSquadron_FM/blob/main/led_blue/Makefile) for building and flashing the Verilog code:

- Run 
```
make clean
```
**to clear any previous builds**

- Run 
```
make build
```
**to compile the design**

- Run 
```
sudo make flash
```
**to program the FPGA board**

Observe the behavior of the RGB LED on the board to confirm successful programming.

## Step 4: Final Documentation

- Compile all observations, explanations, and steps into a comprehensive report.

- Include:

Summary of the Verilog code functionality

Pin mapping details from the PCF file

Integration steps and observations while working with the FPGA Mini board

Challenges faced and solutions implemented

Submit the final document along with the working Verilog and PCF files.

- Document all of these in a GitHub repo.

