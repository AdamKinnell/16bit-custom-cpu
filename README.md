# 16-bit Custom CPU

Custom CPU architecture created in [logisim-evolution](https://github.com/reds-heig/logisim-evolution "logism-evolution").

![](https://raw.githubusercontent.com/AdamKinnell/16bit-custom-cpu/master/img/computer_screenshot.png)

## Background

This was started as a personal project in 2016, in order to understand the details of how logic gates can be combined to create something a complicated as a processor.

It enabled me to experiment with and understand more intricate concepts such as how data flows through the cpu, how the clock drives the components, and considerations when designing a cpu architecture.

## Features
* Custom single cycle RISC Load-Store architecture similar to MIPS.
* 16-bit native word size with 32-bit instruction size.
* 27 instructions supported.
* Separate instruction and data memory.
* Supports programming via direct memory modification.
* Interactive and steppable through logisim.
* Seperated into 54 components to aid abstraction and understanding.
* Implemented entirely through logical primitives,  
although the inbuilt memory cells are used for performance reasons.

## Usage
1. Download [logisim-evolution](https://github.com/reds-heig/logisim-evolution "logism-evolution")
Last tested with version 2.41.6
2. Download `cpu.circ` from this repository.
3. (Optional) Download the basic assembler from [here](https://github.com/AdamKinnell/16bit-custom-cpu-assembler).
4. Run `logisim-evolution` and load `cpu.circ`
5. Enable simulation by selecting to the `Simulate->Simulation Enabled` menu item.
6. Reset the simulation selecting to the `Simulate->Reset Simulation` menu item.
7. (Optional-ish) Generate some assembly code; either manually or through the assembler.  
Refer to the [documentation](https://github.com/AdamKinnell/16bit-custom-cpu/tree/master/doc) for more details.
8. (Optional-ish) Load the instructions via the steps below.
9. Start the clock by selecting the `Simulate->Ticks Enabled` menu item.

By default, the processor will start with the halt instruction at 0x0. (which was *definitely* intentional. yep.)
Therefore, if the instruction memory is not modified, the processor will do nothing.

## Loading programs
1. Go to the `RAM_1KB_A` circuit in the window on the left side of the logisim application.
2. Right-click on the memory bank and go to `Edit Contents...`
3. Enter machine code directly or load it from a file.
4. Memory is updated once the main window is in focus again, no need to close the window or apply changes.

Each group in the hex editor window is 32-bits (1 instruction).  
Input is big-endian, so no need to swap bytes or do anything messy.

You may keep the hex editor open to modify the code as it's being run.

## Images

![CPU Datapath](https://raw.githubusercontent.com/AdamKinnell/16bit-custom-cpu/master/img/cpu_screenshot.png)
Screenshot of the main CPU datapath (the internals of the CPU component shown in the first image).

Each component can be expanded into it's own circuit.

------------

![CPU Controller](https://raw.githubusercontent.com/AdamKinnell/16bit-custom-cpu/master/img/cpu_controller_screenshot.png)
Screenshot of the CPU controller expanded (the internals of the CPU Controller component shown in the previous image).
