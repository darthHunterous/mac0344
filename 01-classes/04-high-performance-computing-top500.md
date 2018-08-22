# Class 04 - High Performance Computing Under Top 500 List

* **Performance Measurement**
    * 1 FLOPS
        * One floating point operation per second
    * **SI Prefixes**
        * Mega = 2^20 ~ 10^6
        * Giga = 2^30 ~ 10^9
        * Tera = 2^40 ~ 10^12
        * Peta = 2^50 ~ 10^15
        * Exa = 2^60 ~ 10^18
        * Zetta = 2^70 ~ 10^21
        * Yotta = 2^80 ~ 10^24
    * 2^10 is approximately 10^3 (1024 ~ 1000)
<br><br>
* **[Top500 List](https://www.top500.org)**
    * Twice a year: June and November
    * Interesting for manufacturers and potential buyers
    * LINPACK Benchmark
        * Solution of a linear system with *n* equations and *n* unknowns
* **June Of 2018 - Number 1**
    * Summit (USA)
    * 4356 nodes
        * Each with 2 Power9 CPUs (22 cores) and 6 NVIDIA Tesla V100 GPUs
    * 3,120,000 cores
    * LINPACK 122.3 PFLOPS
        * Peak speed of 187.6 PFLOPS
* **June Of 2018 - Number 2**
    * Sunway TaihuLight (China)
    * 40960 nodes
        * Each node is a SW26010 1.45 GHz with 260 cores
    * 10,649,600 cores
    * 1.31 PB Memory
    * LINPACK 93.01 PFLOPS
        * Peak speed of 125.43 PFLOPS
* **June Of 2018 - Number 3**
    * Sierra (USA)
        * Architecture similar to Summit's
    * 4320 nodes
        * Eah with 2 Power9 CPUs (22 cores) and 4 NVIDIA Tesla V100 GPUs
    * 1,572,480 cores
    * LINPACK 71.6 PFLOPS
        * Peak Speed of 119.2 PFLOPS
* **Former Champions**
    * **November of 2011**
        * K Computer (Fujitsu Japan)
    * **June of 2010**
        * Jaguar Cray XT5 Opteron
    * **June of 2009**
        * Roadrunner IBM PowerXCell
* **USP - University Of São Paulo**
    * As of November of 2006, USP had a computer at position 363 with 3.182 TFLOPS in LINPACK
    * Got out of the TOP500 in the next list (June of 2007)
* **Analysis of Top500 progression**
    * Top 1 becomes Top500 in around 6 years
* **Domestic Computers Analysis**
    * A domestic mid-end computer with two NVIDIA GeForce GTX-680 (3072 cores, peak of 4.5 TFLOPS) would be Top 1 of the list until November of 2000
        * From 1997 to 2000 Top 1 was the Intel ASCI Red with peak speed of 1.3 TFLOPS
* **Performance Projection**
    * If the current growth was kept during the upcoming years, we would reach a supercomputer with at least 1 ExaFLOPS performance by the year 2020
<br><br>
* **Possible Supercomputer Architectures**
    * Single Processor
    * SMP - Symmetric Multi Processor
    * MPP - Massively Parallel Processor
    * Cluster - Network of Workstations
    * Constelation - Cluster of clusters
* Over the last 10 years, MPP and Cluster architectures have dominated the supercomputers architecture
<br><br>
* **Microeletronics Improvements - VLSI Technology**
    * Hardware Improvements
        * Processing speed
        * Storage
        * Size
        * Price (lower cost)
    * Related to VLSI (Very Large Scale Of Integration)
    * **Silicon Chip**
        * Compose processors and memories
        * Digital circuits basic element
            * MOS - Metal Oxide Semiconductor
                * Kind of interrupting gate around square micrometres of area
                * Electrical charge (high voltage) at the MOS gate allows electrical conduction between D and S points
                * Absence of electrical charges (low voltage) in the gate prevents electrical conduction
<br><br>
* **Moore's Law**
    * Ammount of transistors in a chip doubles each 18 months
<br><br>
* **Size (width) of a MOS Transistor**
    * 1963 - 24 µm
    * 1978 - 5 µm
    * 1990 - 1 µm
    * 2005 - 0.1 µm
* **VLSI Chips - Billions of Transistors**
    * Intel Tukwila Quad-Core (2008)
        * Over 2 billion transistors
        * 65 nm size
    * Intel Core i7
        * 45 nm CMOS
    * Intel Xeon Broadwell - 2016
        * 22 cores
        * 7.2 billion transistors
    * IBM - June of 2017
        * Announced the creation of silicon chip of 5 nm
* **Reflexions about computer evolution**
    * Improvements are related to the VLSI technology
    * **Parallel Computing**
        * One way of improving processor speed is raising its clock speed, reducing the cycle
            * However due to heat dissipation, the frequency isn't rising considerably
        * To solve the incapability of raising clock speed, the way for improvement is adding more cores in a chip

