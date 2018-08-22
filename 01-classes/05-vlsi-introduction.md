# Class 05 - VLSI Technology

* **VLSI**
    * Integrates a big ammount of electronical devices (transistor) in a chip
    * **SSI**
        * Small Scale Of Integration
    * **MSI**
        * Medium Scale Of Integration
    * **LSI**
        * Large Scale Of Integration
    * **VLSI**
        * Very Large Scale Of Integration
<br><br>
* **Electrical vs Hydraulical Analogy**
    * **Electrical Charge**
        * Water Drop
    * **Electrical Current**
        * Water Flow
    * **Voltage**
        * Water Pression
    * **Battery**
        * Pump
    * **Resistor**
        * Turbine
    * **Capacitor**
        * Water Tank
<br><br>
* **MOS Transistor**
    * **MOS**
        * Metal Oxide Semiconductor
    * Current gate made of semiconductor (Silicon Si)
* **MOS Transistor Width - Evolution**
    * **1963**
        * 24 µm
    * **1978**
        * 5 µm
    * **1990**
        * 1 µm
    * **2005**
        * 0.1 µm
    * **2017**
        * 0.01 µm
<br><br>
* **MOS Technology**
    * Simplified with NMOS for better understanding
    * CMOS is the current technology
    * In the Silicon Wafer, three layers of conductor material are stacked in top of each other
        * Metal (Blue colour in drawings)
        * Polysilicon (Red colour in drawings)
        * Diffusion (Green colout in drawings)
    * Each of the three layers are separated by insulating oxide
* **Layer Superposition**
    * A metal trail can cross a polysilicon or difusion trail without significative outcomes
* **Superposition Producing a Transistor**
    * MOS Transistor comes from crossing a **polysilicon** trail with a **diffusion** trail
    * The **polysilicon** trail is separated from the **diffusion** by an oxide, which is the **canal**
    * The **polysilicon** acts as a **gate** separating the **diffusion** trail in points **D** and **S**
    * Suppose that the voltage between points **D (drain)** and **S (source)** isn't null (**V<sub>DS</sub> > 0**)
        * Suppose **V<sub>threshold</sub>** a small threshold voltage, characteristic of the material
        * **Gate without charge**
            * No current through, as the circuit between **D** and **S** is not complete
        * **Charged Gate**
            * Electrons concentrate in the channel (due to electrical attraction), thus current will flow from **D** to **S** if the voltage between the **gate** and **S** is bigger than **V<sub>threshold</sub>**
        * MOS Transistor works as a on-off key
<br><br>
* **Structure for MOS Transistor**
    * **L - Length**
        * Distance between Source and Drain
    * **W - Width**
        * Size of the source and the drain (width of diffusion trail)
* **MOS Transistor as Capacitor, Key and Resistor**
    * MOS Transistor can store electrical charge, acting as a Capacitor
    * Can act also as an on-off key, controlling the current passage
        * Pass Transistor
            * They can implement a multiplexer or selector
    * Even when conducting current, the MOS transistor has a resistance, thus it can act as a resistor
        * Used to build a **NOT** logical port
<br><br>
* **Two transistors as a NOT port**
    * Pull-up transistor (pu)
        * The up transistor, projected to always allow current through
        * Acts as a resistance
    * Pull-down transistor (pd)
        * Acts as a key
    * When voltage in the pull-down transistor gate is smaller than V<sub>threshold</sub>, it works as an open key, thus out Voltage is equal to **VDD**
        * Small voltage in input (zero), V<sub>out</sub> = VDD (one)
    * When voltage in the pull-down transistor gate is bigger than V<sub>threshold</sub>, current flows through it and the pull-down works as resistance
        * If the pull-down transistor resistance is big enough, we have **V<sub>out</sub> \< V<sub>threshold</sub>**
        * Higher voltage in input (one), small voltage in output (zero)
<br><br>
* **MOS Transistor Acting as Resistor**
    * When conducting current, the transistor has a resistance
    * Its value is directly proportional to the length **L** and inversely proportional to width **W**
    * **R = <sup>α\*L</sup>&frasl;<sub>W</sub>**
        * **Length - L**
            * Measured in the direction of the current flux
        * **Width - W**
            * Ortoghonal to Length
<br><br>
* **NOT Port - Transistor Dimensions**
    * Pull-Up Transistor (pu) resistance should be 4 times the resistance of the pull-down transistor (pd)
    * Thus
        * **R<sub>pu</sub> = 4 \* R<sub>pd</sub>**
        * **<sup>L<sub>pu</sub></sup>&frasl;<sub>W<sub>pu</sub></sub> = 4 \* <sup>L<sub>pd</sub></sup>&frasl;<sub>W<sub>pd</sub></sub>**
<br><br>
* **NAND Gate**
    * Similar to the NOT gate, however with two series pull-down transistors
* **NOR Gate**
    * Similar to the NAND gate, however with two parallel pull-down transistors
<br><br>
* **Boolean Logic**
    * **De Morgan's Laws**
        * <span style="text-decoration: overline">X &and; Y</span> = <span style="text-decoration: overline">X</span> &or; <span style="text-decoration: overline">Y</span> 
        * <span style="text-decoration: overline">X &or; Y</span> = <span style="text-decoration: overline">X</span> &and; <span style="text-decoration: overline">Y</span>
    * How to represent two **AND**, both connected to an **OR** with **NANDs**
        * F = (A &and; B) &or; (C &and; D)
        * Negating two times (identity) and applying De Morgan follows:
            * &not;[<span style="text-decoration: overline">(A &and; B)</span> &and; <span style="text-decoration: overline">(C &and; D)</span>]
            * Equivalent to three **NAND** ports
    * Using three **NORs** ports to represent the previous logical equation
        * F = &not;[<span style="text-decoration: overline">(A &and; B)</span> &and; <span style="text-decoration: overline">(C &and; D)</span>] = &not;(&not;A &or; &not;B) &or; &not;(&not;C &or; &not;D)
        * Thus, &not;F = &not;[&not;(&not;A &or; &not;B) &or; &not;(&not;C &or; &not;D)]
            * We obtain &not;F through two **NOR** gates outputs connected to a third **NOR** inputs
            * The two **NOR** gates inputs comes from **NOT** ports
            * As we obtain &not;F, we need just a **NOT** to output F with three **NOR**s
<br><br>
* **Questions**
    * **01**
        * The MOS transistor resistance in the conduction state is not null
        * The resistance is directly proportional to **L**
        * The resistance is inversely proportional to **W**
    * **02**
        * For a **NAND** port we need three transistors
    * **03**
        * For a **NOR** port we also need three transistors
    * **04**
        * Any boolean logic can be implemented with **NOT**, **NAND** and **NOR**