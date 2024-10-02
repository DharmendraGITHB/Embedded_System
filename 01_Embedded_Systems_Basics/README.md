# Embedded Systems Basics

This folder contains materials on the fundamental concepts of embedded systems.

- [Microcontrollers vs Microprocessors](microcontrollers_vs_microprocessors.md): Comparison between microcontrollers and microprocessors.
- [Real-Time Operating Systems](real_time_operating_systems.md): Overview of RTOS and its characteristics.
- [Interrupts](interrupts.md): Explanation of interrupts and their role in embedded systems.
- [Power Management](power_management.md): Techniques and strategies for power management in embedded systems.


# Building Blocks of Embedded Systems

![Building Blocks of Embedded Systems](01_Embedded_Systems_Basics/embedded_system_pics/building_blocks_embedded_systems.png)

## 1. Central Processing Unit (CPU)

The **CPU** is the core of the embedded system, responsible for executing machine instructions. It contains multiple **registers**, **arithmetic logic units (ALUs)**, and control units.

### Components of a CPU:

- **Registers**: Small storage locations within the CPU used for fast data access. Registers store operands for calculations and intermediate results.
  - **Program Counter (PC)**: Holds the address of the next instruction to be executed.
  - **Accumulator (ACC)**: A register used for arithmetic and logic operations.
  - **Instruction Register (IR)**: Holds the current instruction being executed.
  - **Stack Pointer (SP)**: Points to the top of the stack in memory.

- **ALU (Arithmetic Logic Unit)**: Performs mathematical operations (addition, subtraction, multiplication) and logical operations (AND, OR, XOR).
  - Example: If a CPU needs to add two numbers, say \(A = 5\) and \(B = 3\), the ALU fetches the data from registers, adds them, and stores the result back.

- **Control Unit**: Directs the operation of the processor, telling the memory, ALU, and I/O devices how to respond to the instructions.

### Pipeline Architecture (Advanced CPU Design):
Modern embedded CPUs like the ARM Cortex-M series use **pipelining** to improve instruction throughput by executing multiple instructions simultaneously at different stages. For example, while one instruction is being decoded, another can be fetched, and a third can be executed.

#### Mathematical Perspective:
- If a non-pipelined CPU takes 5 clock cycles to complete one instruction and runs at 100 MHz:
  - **Time per Instruction**: \( \frac{5}{100 \times 10^6} = 50 \, \text{ns} \).
- In a 5-stage pipeline, each instruction may only take 1 cycle after the pipeline is filled:
  - **Throughput**: 100 million instructions per second (MIPS).

## 2. Memory

Memory in embedded systems includes **volatile** and **non-volatile** types, each playing distinct roles. The size and type of memory significantly influence the system's performance and energy consumption.

### Types of Memory:

- **RAM (Random Access Memory)**:
  - Used for temporary storage of data, stack, and heap during program execution.
  - **SRAM (Static RAM)**: Faster and consumes less power, but expensive and used in smaller sizes (e.g., 64 KB in microcontrollers).
  - **DRAM (Dynamic RAM)**: Slower and needs constant refreshing but can store more data and is cheaper. Used in larger systems like microprocessors.

- **ROM (Read-Only Memory)**:
  - Stores firmware or boot code that doesn't change frequently.
  - **Mask ROM**: Hardcoded during manufacturing, not changeable.
  - **Flash Memory**: Can be erased and rewritten, making it ideal for systems requiring frequent firmware updates.

### Memory Mapping and Paging:
In embedded systems, **memory-mapped I/O** is a technique where I/O devices are assigned specific memory addresses, allowing the CPU to read/write to I/O devices as if they were memory locations.

#### Mathematical Perspective:
If a system has 64 KB of RAM:
- **Addressable Memory**: \( 2^{16} = 65536 \) bytes (each addressable unit is 1 byte).

For example, if the CPU addresses memory using a 16-bit address bus, it can address up to 64 KB of memory.

## 3. Input/Output (I/O) Interfaces

I/O interfaces allow embedded systems to interact with external hardware devices like sensors, displays, and communication modules. Advanced I/O systems often include **interrupt-driven I/O**, **DMA (Direct Memory Access)**, and **bit-banging**.

### Types of I/O:

- **Polling I/O**: The CPU constantly checks whether the device is ready to send/receive data. This is simple but inefficient.
- **Interrupt-Driven I/O**: The CPU performs other tasks until the device signals it has data (via an interrupt). More efficient but requires proper interrupt handling.
  
- **DMA (Direct Memory Access)**: The CPU can delegate data transfer tasks to the DMA controller, freeing up CPU cycles.

### Communication Protocols:
Embedded systems often need to communicate with other devices using common protocols:
- **UART (Universal Asynchronous Receiver/Transmitter)**: For serial communication.
- **SPI (Serial Peripheral Interface)**: For fast synchronous communication with peripherals (e.g., sensors).
- **I2C (Inter-Integrated Circuit)**: A 2-wire protocol for communication between multiple devices, often used for low-speed peripherals.

#### Mathematical Perspective:
If an I2C bus operates at 100 kHz, and you transmit a 1-byte data (8 bits) followed by an acknowledgment (1 bit), the time for one transaction is:
- **Transmission Time**: \( \frac{9}{100 \times 10^3} = 90 \, \mu \text{s} \).

## 4. Timers and Counters

Timers and counters are critical for managing tasks like generating periodic interrupts, counting events, and producing PWM (Pulse Width Modulation) signals.

### Types of Timers:

- **Basic Timers**: Generate time-based interrupts.
- **PWM Timers**: Used to control the duty cycle of signals, often used in controlling motor speeds or dimming LEDs.

### Advanced Timer Use:
Timers can also be used for **Input Capture** (capturing a signal event) or **Output Compare** (generating a precise signal).

#### Mathematical Perspective:
Consider a 16-bit timer running at 1 MHz:
- **Maximum Timer Value**: \( 2^{16} - 1 = 65535 \) counts.
- **Overflow Time**: \( \frac{65536}{1 \times 10^6} = 65.536 \, \text{ms} \).

## 5. Communication Interfaces

Advanced embedded systems rely heavily on sophisticated communication protocols, allowing them to interact with other devices in a networked environment.

### Protocols in Depth:

- **UART**: Often used for serial communication, UART involves start bits, stop bits, and parity for error detection. Baud rates control the speed of communication.
- **CAN (Controller Area Network)**: Designed for real-time communication in automotive systems. Uses differential signaling to reduce noise and supports multi-master communication.

#### Mathematical Perspective:
For a CAN bus operating at 1 Mbps:
- **Message Length**: 128 bits per message.
- **Throughput**: \( \frac{1 \times 10^6}{128} = 7812.5 \, \text{messages/sec} \).

## 6. Power Supply

Power management is critical in embedded systems, especially in battery-operated devices. The system's design determines how energy-efficient it can be while performing its required tasks.

### Power-Saving Techniques:

- **Sleep Modes**: CPUs often feature different sleep states like idle, deep sleep, and shutdown modes. The system can enter a lower power state when no active processing is required.
- **Dynamic Voltage and Frequency Scaling (DVFS)**: Adjusts the voltage and frequency of the CPU dynamically based on the workload.

#### Mathematical Perspective:
If a system consumes 50 mA at 3.3V:
- **Power Consumption**: \( P = V \times I = 3.3V \times 50 \times 10^{-3}A = 165 \, mW \).

## 7. Real-Time Operating System (RTOS)

An **RTOS** ensures that tasks are completed within their time constraints. It supports **multitasking**, **scheduling algorithms**, and **interrupt handling**.

### Features of an RTOS:

- **Preemptive Multitasking**: Allows higher-priority tasks to interrupt lower-priority tasks.
- **Task Scheduling**: Algorithms like **round-robin** or **rate-monotonic** determine how tasks are prioritized.
- **Inter-Task Communication**: Mechanisms like **semaphores**, **queues**, and **mutexes** are used to synchronize tasks and share data safely.

#### Mathematical Perspective:
Consider a periodic task that must execute every 10 ms on a 16 MHz CPU. If the task takes 5,000 cycles to execute:
- **Execution Time**: \( \frac{5000}{16 \times 10^6} = 0.3125 \, ms \).
- The task must be scheduled with enough margin to complete within the 10 ms period.

## 8. Sensors and Actuators

Embedded systems often interface with physical environments through **sensors** (for data acquisition) and **actuators** (for control).

### Advanced Sensors:
- **MEMS (Micro-Electro-Mechanical Systems)** sensors such as accelerometers and gyroscopes are used in applications like smartphones, drones, and robotics for motion tracking.
  
### Actuators:
- **Servos**: Use PWM signals to control their position.
- **Step Motors**: Use precise control signals to rotate in small increments, often used in robotics.

#### Mathematical Perspective:
If a temperature sensor provides a linear output of 10 mV/°C, and the measured voltage is 0.5V:
- **Temperature**: \( \frac{0.5V}{10 mV/°C} = 50°C \).

## 9. Software/Firmware

Embedded software is written in low-level languages like **C** or **assembly** for tight control over hardware interactions and resource management. The firmware typically includes device drivers, application logic, and often an RTOS.

### Firmware Development:
- **Device Drivers**: Low-level software components that allow the operating system to communicate with hardware devices.
- **Middleware**: Software that sits between the operating system and applications, often handling communication and data management.

### Debugging and Testing:
- Tools like **JTAG** or **SWD (Serial Wire Debug)** interfaces allow developers to debug embedded software in real-time.

### Code Optimization:
Optimizing firmware for performance and memory usage is crucial, especially in resource-constrained environments.

#### Mathematical Perspective:
If a microcontroller has 64 KB of flash memory and the firmware uses 32 KB:
- **Memory Utilization**: \( \frac{32 \, \text{KB}}{64 \, \text{KB}} \times 100 = 50\% \).
