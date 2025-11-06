
### **CPU Core Concepts**
* **Central Processing Unit (CPU):** The “brain” of the computer. Executes instructions from programs using its internal components It is the primary processor in a given computer.
* **Instruction:**  A low-level operation (like `ADD`, `LOAD`, or `JUMP`) that the CPU understands and executes.
- **Clock / Clock Speed:**  The rate (in Hz or GHz) at which the CPU executes instructions. 
- **Cycle:**  A single tick of the CPU clock — each instruction takes one or more cycles to complete depending on its complexity.
### **Caching & Memory Hierarchy**
- **Cache:**  Small, fast memory close to the CPU that stores frequently used data or instructions. 
- **Cache Miss:**  When data isn’t found in the cache, forcing a fetch from slower memory.
- **Cache Line:**  The basic unit of data transferred between memory and cache (often 64 bytes).
- **Memory Latency:** how long it takes to access data.
- **Memory Bandwidth:** how much data can be moved per unit time.

| Cache  | Location         | Typical Size | Access Speed  | Shared By           | Purpose                                                                                        |
| :----- | :--------------- | :----------- | :------------ | :------------------ | :--------------------------------------------------------------------------------------------- |
| **L1** | Inside each core | ~32–64 KB    | ~1–4 cycles   | One core            | Holds the most immediately needed instructions and data. Extremely fast.                       |
| **L2** | Inside each core | ~256 KB–1 MB | ~10 cycles    | One core            | Larger and slower than L1. Stores data recently used but not currently “hot.”                  |
| **L3** | On the CPU chip  | ~4–64 MB     | ~30–50 cycles | Shared by all cores | Acts as a “last resort” before going to main memory (RAM). Helps with inter-core data sharing. |
|        |                  |              |               |                     |                                                                                                |
**Caches exist to hide the slowness of memory.**

Accessing data from main memory (RAM) takes **hundreds of CPU cycles** — an eternity for the processor.

**orders of magnitude longer**:
L1: 1 ns L2: 4 ns L3: 10–20 ns RAM: 100 ns Disk (SSD): ~100,000 ns Disk (HDD): ~10,000,000 ns`

That’s why **locality** matters: CPUs and compilers try to reuse data that’s already in cache (temporal locality) and access nearby memory (spatial locality).

**Caches exist to hide the slowness of memory.**

Accessing data from main memory (RAM) takes **hundreds of CPU cycles** — an eternity for the processor.


## Memory vs Disk Space

This distinction often confuses beginners — because both “store data,” but they serve _different roles_ in the system.

| Feature        | **Memory (RAM)**                                  | **Disk Storage (SSD/HDD)**                |
| :------------- | :------------------------------------------------ | :---------------------------------------- |
| **Purpose**    | Temporary workspace for running programs and data | Long-term data storage                    |
| **Volatility** | **Volatile** — loses data when power is off       | **Non-volatile** — data persists          |
| **Speed**      | Very fast (tens to hundreds of ns access)         | Very slow (microseconds to milliseconds)  |
| **Capacity**   | Smaller (GBs)                                     | Much larger (hundreds of GBs to TBs)      |
| **Used by**    | CPU during program execution                      | OS & user to store files, apps, databases |
| **Example**    | Variables in memory while program runs            | Saved documents, videos, database files   |
### Why the distinction matters for systems design

- **Performance:** RAM is thousands of times faster than disk → caching layers (both CPU-level and application-level) exist to avoid slow disk access.
    
- **Persistence:** RAM is temporary, so databases and OSs must write important data back to disk to survive crashes.
    
- **Scaling:** Systems often use **distributed caches (like Redis or Memcached)** to mimic “RAM-like” speed at scale, avoiding slow disk I/O on each request.


### **Parallelism**
- **Core:**  
    A single processing unit within a CPU chip. Multi-core CPUs can run multiple threads simultaneously.
- **Thread:**  
    A sequence of programmed instructions that can be managed independently. Multiple threads may share CPU cores.
- **Hyper-Threading (Simultaneous Multithreading, SMT):**  
    Allows one physical core to appear as multiple logical cores, running two (or more) threads interleaved on the same hardware resources.
- **Vectorization / SIMD (Single Instruction, Multiple Data):**  
    One instruction operates on multiple data points at once (useful in multimedia, AI, scientific workloads).

### **Performance & Optimization**

- **Throughput:**  
    Amount of work done per unit time. Often improved with parallelism.
- **Latency:**  
    Time it takes to complete a single task or operation.
- **Instruction-Level Parallelism (ILP):**  
    Parallel execution of independent instructions in the same thread.
- **Branch Prediction:**  
    CPU guesses which way a branch (e.g., an if-statement) will go to avoid pipeline stalls.
- **Speculative Execution:**  
    CPU executes instructions ahead of time based on predictions; if the prediction was wrong, results are discarded.
