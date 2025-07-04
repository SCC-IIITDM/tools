# tools
# Verilator + GTKWave: Getting Started on Ubuntu

This guide walks you through installing **Verilator** and **GTKWave** on Ubuntu, writing a simple Verilog module (an OR gate), testing it with a testbench, simulating it using Verilator, and viewing waveforms using GTKWave.

---

## ✅ Step 1: Install Verilator and GTKWave

### Open a terminal and run:

```bash
sudo apt update
sudo apt install verilator gtkwave
```

### Check if Verilator is installed:

```bash
verilator --version
```

---

## 🧰 Step 2: Set Up the Project

Create a folder for your project:

```bash
mkdir or_gate_test
cd or_gate_test
```

---

## ✍️ Step 3: Write the OR Gate Module

Create a file called `or_gate.v`:

```verilog
module or_gate (
    input wire a,
    input wire b,
    output wire y
);

assign y = a | b;

endmodule
```

---

## 🧪 Step 4: Write a Testbench

Create a file called `tb_or_gate.v`:

```verilog
`timescale 1ns/1ps

module tb_or_gate;

    reg a, b;
    wire y;

    // Instantiate the OR gate
    or_gate uut (
        .a(a),
        .b(b),
        .y(y)
    );

    // Dump waveform for GTKWave
    initial begin
        $dumpfile("dump.vcd");
        $dumpvars(0, tb_or_gate);
    end

    // Apply test cases
    initial begin
        a = 0; b = 0; #10;
        a = 0; b = 1; #10;
        a = 1; b = 0; #10;
        a = 1; b = 1; #10;
        $finish;
    end

endmodule
```

---

## ⚙️ Step 5: Compile and Run the Simulation

Run the following command to compile using Verilator:

```bash
verilator -Wall --cc or_gate.v --exe tb_or_gate.v --build
```

Now run the compiled testbench:

```bash
./obj_dir/Vtb_or_gate
```

This will create a file named `dump.vcd` which contains the simulation waveform.

---

## 👁 Step 6: View Waveform in GTKWave

Open the waveform file using GTKWave:

```bash
gtkwave dump.vcd
```

Once GTKWave opens:

1. Add signals from the left pane to the waveform view
2. Click "Run" or use the time navigation controls to observe signal transitions

You should see the values of `a`, `b`, and `y` changing over time based on the OR logic.

---


