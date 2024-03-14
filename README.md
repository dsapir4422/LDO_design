# LDO_design
In This project I will show a Low Drop Out (LDO) voltage regulator from 1.8[V] -> 1.5[V] with a PMOS pass element. 
The LDO circuit consist of the following sub-circuits: 
* Single stage opamp - LDO error amplifier
* Beta multiplier - for suppling current to opamp
* Bandgap - for suppling the single stage opamp reference voltage
**********

## Design calculations
The LDO output voltage is defined as $V_{out} = V_{ref} * (1+R_1/R_2)$, for a 1.5[V] we will choose $R_1 = 30K$ and $R_2 = 120K$.
The pass element should handle large current and therefore should be width -> W = 8u.



