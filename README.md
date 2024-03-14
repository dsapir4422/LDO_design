# LDO_design
In This project I will show a Low Drop Out (LDO) voltage regulator from 1.8[V] -> 1.5[V] with a PMOS pass element. 
The LDO circuit consist of the following sub-circuits: 
* Single stage opamp - LDO error amplifier
* Beta multiplier - for suppling current to opamp
* Bandgap - for suppling the single stage opamp reference voltage
**********

## Design calculations & consideration
The LDO output voltage is defined as $V_{out} = V_{ref} * (1+R_1/R_2)$, for a 1.5[V] we will choose $R_1 = 30K$ and $R_2 = 120K$.
The pass element (PMOS) should handle large current and therefore should be width -> W = 8u.

The error amplifier is a 5T-OTA single stage amplifier with 1 pole (and therefore stable by design) and have a decent 30dB open-loop gain
  - More elaborated design details can be found here - [Single stage 5T-OTA](https://github.com/dsapir4422/5T_OTA/blob/main/README.md)

The Beta multiplier supply 10[uA] to the error amplifier and has a start-up circuit, the current can be calculated as - $I_{out} = (2/U_nC_{ox}R_s^2)*(1-1/\sqrt(K))^2$

The bandgap supply 1.2[V] for the error amplifier as reference voltage for the LDO close-loop.
  - More elaborated design details can be found here - [BandGap-cell-with-opamp-feedback](https://github.com/dsapir4422/BGAP-cell-with-feedback/blob/main/README.md)

We will compare ideal voltage/current LDO behavior vs. real voltage/current from the above circuits.
**********

## LDO circuit and sub blocks
Ideal circuit - 
<img width="935" alt="image" src="https://github.com/dsapir4422/LDO_design/assets/87266625/7316f66a-2607-47c1-86b2-93b042bfbc35">


Final circuit with non-ideal sub-circuits - 
<img width="935" alt="image" src="https://github.com/dsapir4422/LDO_design/assets/87266625/bb910958-97fa-4143-b9b2-4a286dcc9c1f">


Beta-multiplier - 
<img width="935" alt="image" src="https://github.com/dsapir4422/LDO_design/assets/87266625/830a86ec-c168-48f5-a825-9ae7129e8655">


Bandgap - 
<img width="935" alt="image" src="https://github.com/dsapir4422/LDO_design/assets/87266625/9cbef59d-a317-4713-bf56-cb45acb13d8e">


Error amplifier - 
<img width="935" alt="image" src="https://github.com/dsapir4422/LDO_design/assets/87266625/da7aabb1-850a-4d0e-b82c-7d4064df81db">


## Simulation results
**Line regulation simulation**, ideal vs. non-ideal. we can see a maximum of 200mV (SS corner) change over a range of 1.6-2.0[V] in VDD. which can be improved by a more robust design for the sub-circuits over corners - 
<img width="997" alt="image" src="https://github.com/dsapir4422/LDO_design/assets/87266625/88bd36dd-4975-420f-b9a3-35755ec86b54">

Error amplifier Open-loop gain and Phase-margin - 
<img width="997" alt="image" src="https://github.com/dsapir4422/LDO_design/assets/87266625/d60ba01b-3075-42d5-ab07-6187ed092390">

**Beta-multiplier start-up circuit** -  
M6 NMOS should supply the start-up voltage for the circuit. we can see on t=0 M6 drain (vpmos) is larger than M6 source (vnmos) and therefore Ids is flowing on this branch (I4), but after 6[ns], the drain voltage started to drop and source voltage starts to increase -> $I_{M6}$ drop and M6 change from saturation to cut-off, causing the beta-multiplier transistors to start in saturation -> $I_{M3,M1}$ converge to 10[uA] - 
<img width="989" alt="image" src="https://github.com/dsapir4422/LDO_design/assets/87266625/a7fb0ab7-e6fb-45f2-88ff-dda5acb71313">

Bandgap PTAT/CTAT and VREF - voltage change of 80mV over -40:125[C], this can be improved by a more robust design
<img width="989" alt="image" src="https://github.com/dsapir4422/LDO_design/assets/87266625/18de6604-a827-4e56-ba1b-73be41f3563c">









