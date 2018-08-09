# 02 - Computer Evolution
## From Abacus to ENIAC to Sunway

* **Computer Generations:**
    * First Generation
        * Valves
    * Second Generation
        * Transistors
    * Third Generation
        * VLSI integrated circuit
* **Evolution Consequences:**
    * Raise in processor speed
    * Reduction in components size
    * Raise in I/O capacity and speed
* **Evolution Causes:**
    * Main reason is the reduction of the transistor size
    * **Moore's Law:**
        * The ammount of transistors in a silicon chip doubles every 18 months
    * Processors have been improving
        * Pipelining
        * Superscalar
        * Branch Prediction
        * Speculative Execution
        * Multicore
        * Parallel Programming
* **Need for balancing performance**
    * Processor speed raises quicker than memory access time
        * Techniques have to compensate for that difference
            * Cache
            * Bigger bandwidth between processor and memory
<br><br>
* **Pre-Computer History**
    * **Ancient Abacuses**
        * Mesopotamia abacus
            * 2700 - 2300 B.C.
        * Roman abacus
            * First Century A.D.
        * Chinese abacus
            * 2696 - 2598 B.C.
            * It appears in the table of an apothecary in the painting *Along the River during the Qingming Festival* (12th Century)
    * **Bagua and Binary System**
        * Zhou dinasty (1046 B.C. - 256 B.C.)
        * Book *I Ching* (Book of Mutations)
            * Was either an oracle as a wisdom book
            * Leibniz developd binary arithmetic in 1703 based in *I Ching*
    * **Slide Rules**
        * 17th Century
        * Based on logarithms
<br><br>
* **Zero Generation - Mechanical Computers**
    * 1642 - 1945
    * Wilhelm Schickard - 1623
    * Pascal - 1645
    * Charles Babbage
        * 1792 - 1871
        * Difference Engine
            * Only one algorithm, calculus of maritime navigation tables
        * Analytical Engine
            * General use, but wasn't operational
            * 4 parts
                * Storage
                * Computing
                * Input
                * Output
            * First programmer
                * Ada Lovelace
    * H. Aiken - MARK I (1944)
        * Mechanical relays
        * Clock cycles of 0.3 seconds
<br><br>
* **First Generation - Valves**
    * 1945 - 1955
    * Colossus (1943)
        * Built by the british government to decode ENIGMA's messages
    * ENIAC (1946)
        * Mauchley and Ecker
            * University of Pennsylvania
            * Later founded UNIVAC
        * 18 thousand valves programmed by 6 thousand keys
        * 30 tons
        * Clock speed of 5 kHz
            * 200 micro-seconds of cycle
    * EDSAC (1949)
        * Wilkes
        * First computer with a stored program
    * IAS (1952)
        * Von Neumman
        * Von Neumman's Architecture
            * Memory
            * Processor
            * Control
            * Input
            * Output
    * IBM 701 (1953)
        * First of a series of scientific machines
<br><br>
* **Second Generation - Transistors**
    * 1955 - 1964
    * Transistor, resistor, capacitor
    * IBM 1620
        * First USP's computer (1962)
        * Magnetic-Core memory of 100 thousand bits (12,5 kB)
        * Input and output through punched cards
        * Complicated procedure to execute a program
            * Codification sheet
            * Then, typist would decode from the sheet to the punched cards
            * Batch processing
            * In case of errors, the process would have to be redone, with one less credit for the assignment
    * DEC PDP-1 (1960)
        * First microcomputer with at least 50 units sold
    * IBM-1401 (1961)
        * Small comercial computer with huge success
    * IBM-7094 (1962)
        * Computer for scientific applications
    * Burroughs B-5000 (1963)
        * Designed for high-level language Algol 60
    * Control Data CDC-6600 (1964)
        * Uses multiple functional units
        * Precursos of the superscalar architecture
<br><br>
* **3rd Generation - Integrated Circuits**
    * 1964 - 1980
    * Jack Kiby (1958) from Texas Instruments
        * Produced the first integrated circuit reuniting transistors, resistors and capacitors in a semiconductor chip
        * Physics Nobel prize in 2000
    * IBM-360 (1964)
        * Microprogram machine
        * First of a family
    * Digital PDP-8 (1965)
        * First minicomputer with great sales figures (50 thousand units)
    * Digital PDP-11 (1970)
        * Minicomputer of great success in the 70s
<br><br>
* **4th Generation - VLSI**
    * From 1980 to Present Day
    * VLSI
        * Very Large Scale of Integration
            * Microeletronics technique of implementing micro-components in silicon
        * Revolution in eletronics, responsible for the improvements we've seen until today
    * First Personal Computers appeared at the end of the 70s
    * Two families of processors
        * Intel
        * Motorola
    * Processor in a single chip with millions of transistors
        * Pentium 4 with 42 million transistors
    * 2016 - Intel Xeon Broadwell-EP
        * 22 cores
        * 7.2 billion transistors
<br><br>
* **First IME-USP microcomputer**
    * Prológica S700 (1982-1983)
        * Z-80 processor (8 bits)
        * Borrowed to IME for an year
            * Courtesy of Prológica
* **Second IME-USP microcomputer**
    * Scorpus Nexus 1600 (1984)
        * Intel 8088 (16 bits)
        * 8 MHz
        * 704 kB RAM
        * Two 5 1/4" floppy disk drives
<br><br>
* **Storage Devices**
    * 8" floppy disk
        * 175 kB
    * 5 1/4" floppy disk
        * 360 kB
            * 180 kB each side
    * 3 1/2" floppy disk
        * 1.44 MB
    * CD/DVD disk
<br><br>
* **Computer Evolution**
    * Cycles
        * Mark I: 0.3s cycle
        * ENIAC: 200 micro-seconds cycle
        * Today's processor: GHz clock
            * Less than a nanosecond cycle
        * Today's processor is 100 million times faster than Mark I and 1 million times faster than ENIAC
    * Parallel computation uses a big ammount of processors, expanding processing power
    * TOP500 list
        * 500 fastest computers in the world, based in Linpack benchmark
        * Performance measured in FLOPS
            * Floating Point Operations per Second
<br><br>
* **Fastest Computer in TOP500 list**
    * As of June, 2017, number 01 is the Sunway computer
    * Sunway TaihuLight (China)
    * 40,960 **SW26010** nodes
        * 1.45 GHz each, with 260 cores
    * 10,649,600 cores
    * 1.31 PB RAM
    * LINPACK
        *93.01 PFLOPS
    * Peak performance speed
        * 125.42 PFLOPS
* **Architecture of a SW26010 node**
    * Node
        * Composed of 4 groups
            * Each with 8x8 cores and a Master Core
        * Total of 260 cores
            * Peak speed of 3 TFLOPS
    * TianHe system used Intel processors
    * SW26010 was designed by Shanghai High Performance IC Design Center
* **Sunway Card**
    * Composed by 2 nodes
    * 2 * 260 = 520 cores
* **Sunway Plate**
    * Composed by 4 cards
    * 4 * 520 = 2080 cores
* **Sunway Supernode**
    * Composed by 32 Plates
    * 32 * 2080 = 66,560 cores
* **Sunway Cabinet**
    * Composed by 4 supernodes
    * 4 * 66,560 = 266,20 cores
* **Sunway System**
    * Composed by 40 cabinets
    * 40 * 266,240 = 10,649,600 cores
<br><br>
* **Upcoming Computing**
    * EXAFLOPS Computing
    * New technologies after VLSI
* **Albert Einstein**
    * *Computers are incredibly fast, accurate and stupid: humans are incredibly slow, innacurate and brilliant; together they are powerful beyond imagination*
* **Exercises**
    * Check the fastest computer in Top500 in November of 2018
    * As of June 2018, the fastest brazilian computer is at rank 199
        * BC1 - Lenovo C1040