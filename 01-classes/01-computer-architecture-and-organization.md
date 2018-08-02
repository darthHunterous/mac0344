# 01 - Computer Architecture vs Organization

* **Architecture:**
    * System attributes visible to the machine language programmer
* **Organization:**
    * Operational units and its connection to the architecture
<br><br>
* **Structure:**
    * How components are connected
* **Function:**
    * How each component works
* Components can be split into subcomponents, each with its structure and function
<br><br>
* **Performance:**
    * Processor speed
    * Memory speed and capacity
    * Speed of data connections
<br><br>
* **Computer Architecture:**
    * System attributes related to the programmer
    * Impact directly at the program execution
    * **Examples:**
        * Instruction sets
        * Number of bits to represent data types
        * Input/Output
        * Memory addressing techniques
* **Computer Organization:**
    * Operational units and its connections, which address the architectural specifications
    * **Examples:**
        * Hardware details
        * Control signals
        * Interface between the computer and peripherals
        * Memory technology implemented
* **Example:**
    * It is an **architectural** feature whether a computer should have or not a multiplication instruction
    * However, how this instruction should be implemented is **organizational**
        * It could be implemented with a multiplication unit or repeated use of a addition unit
    * Manufacturers offer processors with the same architecture, differing in its organization
        * They are capable of executing the same programs
        * However, they are models of different performances and prices
<br><br>
* **Hierarchical description of a computer:**
    * One **level** each time, focusing on each of its components and its interconnections
    * **Top-down** approach
        * Describes one level, then its sublevels
* **Structure:**
    * How components are related between them
* **Function:**
    * Operation of each component as part of the structure
    * **Examples:**
        * Data storage
        * Data transfer
        * Data processing
        * Control
<br><br>
* **Computer:**
    * **Input/Output**
        * Transfer data between computer and external environment
        * **Interconnection system**
            * Communication between I/O, Memory and Processor
                * Through the bus, number of parallel lines
            * **Memory**
                * Store data
            * **Processor (CPU - Central Processing Unit)**
                * Controls the computer operation and data processing
<br><br>
* **Processor:**
    * **Internal connection system:**
        * Intercommunicates the control unit, ALU and registers
        * **Registers**
            * Internal storage for the CPU
        * **Control Unit**
            * Controls CPU operation
        * **ALU (Arithmetic Logic Unit)**
            * Operations for data processing
<br><br>
* **Control Unit:**
    * Provides control signals for the coordination of all processor components
        * Implemented through microprogramming (CISC)
    * [Useful Link](https://thalibriyadblog.wordpress.com/2014/09/21/control-unit-in-cpu-sequencing-logic-control-unit-registers-and-decoders-control-memory/)
    * **CISC:**
        * **Sequencing Logic**
            * Logic circuit whose output depends on the past history of its inputs
            * Combinational logic output depends only on the present input
            * So, sequential logic is combinational logic with memory
            * Finite state machines, used in digital and memory circuits
            * Synchronous and asynchronous
                * **Synchronous:** respond only to the clock signal
                    * Simplicity
                    * Propagation Delay
                        * Logic gates take a finite ammount of time to respond to changes in the inputs
                    * Interval between pulses must be long enough to allow logic gates to respond
                        * Guarantees to be stable and reliable
                * **Asynchronous:** respond to changes in the inputs
        * **Control Unit Registers and Decoders**
            * Instruction register, program counter and instruction decoder
            * **Program Counter:**
                * Stores the position of the next instruction
            * **Instruction Register:**
                * Stores current instruction
            * **Instruction Decoder:**
                * Determines what operation to perform based on instruction
        * **Control Memory**
            * Control unit initiate sequences of microoperations
    * RISC is a more recent alternative to CISC

* **Exercise:**
    * Classify the items as related to architecture or organization in a computer
        1. Double float number representation
            * Architecture
        2. Priority levels in the execution of a process
            * Architecture
        3. Implementation of the sum circuit with the "carry-lookahead" technique
            * Organization
        4. Set of instructions in a machine
            * Architecture
        5. How to implement the set of instructions
            * Organization
        6. Using a co-processor for floating point arithmetic
            * Organization
        7. Using a co-processor for image processing
            * Organization
        8. Addressing techniques
            * Organization
        9. Using cache memory to speed up access
            * Architecture/Organization
        10. Adopt an automatized memory access error correction technique
            * Organization  
    * What's the structure of a processor?
    * What's the function of a processor?