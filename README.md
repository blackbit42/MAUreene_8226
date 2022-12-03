# Token Ring MAU 'MAUreen'

MAUreene 8226 is a Token Ring (IEEE 802.5) Media Access Unit (MAU) that is inspired by the IBM 8226. For the most part, it is a reproduction of the IBM 8226, reduced to 2 'lobes', which is Token Ring lingo for what is known as a port in the context of other network technologies.

## Motivation

Token Ring is an interesting LAN technology. NICs are all over common auction sites and can be had cheaply, though MAUs are hard to come by. The intent of this project is to enable inclined people to play with Token Ring more easily.

## Clarification regarding 'crossover' cables

In an ethernet network you can nowadays connect two arbitrary devices with each other back to back without thinking about it, due to to the power of Auto MDI-X. Earlier you could use so-called 'crossover' cables. Unfortunately Token Ring doesn't support such a mode of interconnection, as a NIC goes through a mildly elaborated attachment process with a MAU. A mode where two hosts talk directly to each other doesn't exist, see [this](https://www.tavi.co.uk/ps2pages/ohland/8228.html#DirectCable).

## BOM analysis and mapping

| Original 8226 | Port 1 | Port 2  | Package      | Type                      | Measured value[^1] | Marking           | Remarks                             |
| ---           | ---    | ---     | ---          | ---                       | ---                | ---               | ---                                 |
| R2            | R1     | R21     | 0805         |                           | 4.8k               | 4871              |                                     |
| R10           | R2     | R22     | 0603         |                           | -None-             | -None-            | Opto-coupler biasing, not populated |
| R34           | R3     | R23     | 0603         |                           | 0.3                | 000               | RJ45 termination                    |
| R35           | R4     | R24     | 0603         |                           | 0.3                | 000               | RJ45 termination                    |
| R44           | R5     | R25     | 0603         |                           | 100                | 101               |                                     |
| R52           | R6     | R26     | 0603         |                           | 100                | 101               |                                     |
| R60           | R7     | R27     | 0603         |                           |                    | 104               |                                     |
| R68           | R8     | R28     | 0603         |                           | 10k                | 103               |                                     |
| R76           | R9     | R29     | 0603         |                           | 2k                 | 202               |                                     |
| R84           | R10    | R30     | 0805         |                           | 3.7k               | 3741              |                                     |
| R92           | R11    | R31     | 0603         |                           | 4.7k               | 472               | LED series resistor                 |
| R96           | R12    | R32     | 0603         |                           | 0.3                | 000               | RJ45 termination                    |
| R97           | R13    | R33     | 0603         |                           | 0.3                | 000               | RJ45 termination                    |
| C4            | C1     | C21     | 1812         | Ceramic                   | 330n               | -None-            |                                     |
| C12           | C2     | C22     | 1812         | Ceramic                   | 330n               | -None-            |                                     |
| C20           | C3     | C23     | EIA 7343-31  | Tantalum                  | 22u                | 22-20 LD (2)      |                                     |
| C34           | C4     | C24     | 0805         | Ceramic                   | 120n               | -None-            |                                     |
| C41           | C5     | C25     | 0805         | Ceramic                   | 120n               | -None-            |                                     |
| Q13           | Q1     | Q21     | SOT23        | BJT NPN                   |                    | 1P                |                                     |
| Q14           | Q2     | Q22     | SOT23        | BJT NPN                   |                    | 1P                |                                     |
| CR7           | D1     | D21     | SOT23        |                           | 0.6                | A66 (?)           | Flyback diode for coil in K2        |
| K2[^2]        | K1     | K21     | Non-standard | 4PDT                      |                    | P&B T84S17D214-12 |                                     |
| T2            | T1     | T21     | Non-standard | Special Token Ring        |                    | Valor PT4043      |                                     |
| DS2           | -None- | -None-  | Non-standard |                           |                    | -None-            | LEDs of J1A and J1B are used        |
| L2            | -None- | -None-  | -None-       | -None-                    |                    | -None-            | Unpopulated                         |
| U2            | U1     | U21     | DIP-6        | Opto-Coupler              |                    | QTC H11A1         |                                     | 
| -None-        | J1A    | J1B     | Non-standard | RJ45 jack                 |                    |                   |                                     |

## Power supply BOM

| Part designator | Value  | Description    |
| ---             | ---    | ---            |
| J200            |        | Barrel jack    |
| J201            |        | 2x2 jumper 12V |
| J202            |        | 2x2 jumper 5V  |
| U200            |        | 5V linear reg. |
| C200            | 0.33uF |                |
| C201            | 0.1uF  |                |
| C202            | 0.1uF  |                |
| R200            | 495Ohm | 12V rail ind.  |
| R201            | 145Ohm | 5V rail ind.   |

[^1]: Capacitors have been desoldered for measurement with HP 4262A LCR meter.
[^2]: The polarity of the coil supply is reversed, both in the original and this design. Irrelevant, as the relay coils do not have series diodes.

## Diode direction
CR7 is in a 3-pin SOT23 package, containing only a single diode. It is connected in parallel with a relay coil, indicating reverse EMF protection for adjacent devices in the circuit.
Unfortunately somebody got the direction wrong, hence there is significant reverse EMF with spikes of around 200V. 
Remarkably, neither the diode itself dies from excessive forward current when the relay is on, nor the switching transistor from the voltage spikes when the relay is being switched off.
In the design of this contraption, a diode with normal flyback operation has been foreseen.

## Links

<https://www.ieee802.org/5/www8025org/>

<https://ardent-tool.com/network/Understanding_Token_Ring.html>
