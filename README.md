# Single-Core Processor Simulation & Analysis

## Overview
This project simulates the operation of a single-core processor, managing various processes through different states and handling I/O operations. The simulation is implemented in C++, with an automated Python script (Jupyter Notebook) handling process generation, execution, and comprehensive data analysis. This setup allows for a randomized, end-to-end evaluation of processor behavior and process states.

---

## Methodology & Automation

The core of this project lies in its automated workflow, orchestrating randomized process creation, simulation execution, and detailed data analysis, all managed within a Jupyter Notebook.

### 1. **Process List Generation**
The Jupyter Notebook initiates the simulation by programmatically generating a `procList.txt` file. This file defines a set of processes, each with a unique ID, required processor time, and a series of I/O events (time into execution and duration). The number of processes and their characteristics are randomized for varied simulation scenarios.

![Proc List Input](imgs/Screenshot%202025-05-07%20224637.png)

### 2. **Processor Simulation**
The generated `procList.txt` then serves as input for the C++ simulation. This C++ program models a single-core processor, managing processes through distinct states:
* **Ready (r)**: Processes awaiting processor allocation.
* **Processing (p)**: The process currently utilizing the CPU.
* **Blocked (b)**: Processes waiting for I/O operations to complete.
* **New Arrival (n)**: Newly admitted processes.
* **Done (d)**: Processes that have completed execution.

The simulation meticulously tracks each process's state at every time step, outputting this granular data to `procList_output.txt`. This output is crucial for subsequent analysis.

### 3. **Data Analysis & Visualization**
The Jupyter Notebook then reads the `procList_output.txt` to parse the simulation logs. It calculates the total distribution of time spent by processes in each state (`b`, `d`, `n`, `p`, `r`) across the entire simulation. This data is presented in a clear tabular format referenced in the image below.

Furthermore, the notebook generates two key visualizations:
* **Event Runtime Bar Graph**: This bar chart illustrates the frequency of different event types (`[admit]`, `[begin]`, `[ioReq]`, `[finish]`, `[inrtpt]`, `[contRun]`) that occurred during the simulation.

* **Process State Distribution (Stacked Bar Graph)**: This visualization displays the proportion of time each individual process spent in the Blocked, Done, Processing, and Ready states throughout its lifecycle. This provides a clear overview of resource utilization and process flow.

![Event Runtime Bar Graph](imgs/Screenshot%202025-05-07%20225346.png)

### **Example Simulation Output**

The output below showcases a snippet of the `procList_output.txt` file, demonstrating how process states are logged at each time step.

![Screenshot of procList_output.txt](imgs/Screenshot%202025-05-07%20225253.png)

---

## Technical Skills & Tools

This project showcases proficiency in:
* **C++ Programming**: Development of the core processor simulation logic, including process management, state transitions, and I/O handling.
* **Object-Oriented Design**: Utilization of `Process` and `IOModule` classes to structure the simulation components.
* **File I/O**: Reading process definitions from a file (`procList.txt`) and writing simulation logs to another (`procList_output.txt`).
* **Data Structures**: Effective use of `std::list` for process queues and interrupts, and `std::vector` for pending I/O requests.
* **Python (Jupyter Notebook)**: Scripting for automated process generation, execution of the C++ simulation, and data parsing/analysis using `pandas`.
* **Data Visualization**: Generating insightful plots with `matplotlib` to interpret simulation results.
* **Command-Line Automation**: Executing compiled C++ binaries from within the Python environment.

---

## Findings & Insights

The automated nature of this project allowed for rapid iteration and analysis of different process scenarios. Through the visualizations, we can readily observe:
* The dynamic transitions between process states, such as a process moving from `newArrival` to `ready`, then to `processing`, and potentially to `blocked` upon an I/O request, before finally becoming `done`.
* The impact of I/O bound vs. CPU-bound processes on overall processor utilization and process queueing.
* The effectiveness of the implemented scheduling logic (FIFO in this case) in managing concurrent processes and interrupts.

This project provided a hands-on understanding of operating system concepts related to process scheduling, resource management, and I/O handling in a simulated environment.
