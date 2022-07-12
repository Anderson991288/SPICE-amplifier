# SPICE-Amplifier
## Current Mirror-BJT

![Screenshot from 2022-07-11 22-14-01](https://user-images.githubusercontent.com/68816726/178284813-dd7392ba-9e6c-4e33-947a-564474232565.png)

netlist:
```
A Conventional BJT Current Mirror
* circuit description *
Vcc 1 0 dc 15V
Vo 3 0 dc 3V
R1 1 2 14.3k
* BJT model description
Q1 2 2 0 0 npn_transistor
Q2 3 2 0 0 npn_transistor
.model npn_transistor npn (Is=1.8E-15 BF=100 VAF=100)
* analysis requests
.dc Vo 0V 6V 10mV
.control
run
* output requests *
plot -i(vo)
.endc
```

![Screenshot from 2022-07-11 22-24-28](https://user-images.githubusercontent.com/68816726/178287068-c0023f4b-b3eb-41bf-99a7-a9e16ae49dc5.png)

## Current Mirror-MOS

![Screenshot from 2022-07-12 17-54-39](https://user-images.githubusercontent.com/68816726/178464270-45ecb8da-83de-4c31-8c65-b57e206b9919.png)

netlist
```
Output Characteristics of MOS Cascode Current Mirror Circuit
* circuit description *
Vdd 1 0 dc 15V
vo 4 0 dc 5V
Iref 1 2 dc 1mA
* MOSFET model description
M1 3 3 0 0 nmosfet L=10u W=100u
M2 5 3 0 0 nmosfet L=10u W=100u
M3 2 2 3 0 nmosfet L=10u W=100u
M4 4 2 5 0 nmosfet L=10u W=100u
.model nmosfet nmos (kp=20u Vto=+1V lambda=0.02)
* analysis requests
.dc vo 0V 12V 10mV
.control
run
* output requests
plot -i(vo)

plot v(2)-v(4) v(3)-v(5)
.endc
```
![Screenshot from 2022-07-12 17-54-14](https://user-images.githubusercontent.com/68816726/178464392-0ffd5cfe-3f08-4713-b20d-06f27cb8f482.png)

## 使用tsmc 180nm MOS 模擬
```
Output Characteristics of MOS Cascode Current Mirror Circuit
* circuit description *

.include tsmc018.lib

Vdd 1 0 dc 15V
vo 4 0 dc 5V
Iref 1 2 dc 1mA
* MOSFET model description
M1 3 3 0 0 CMOSN 
M2 5 3 0 0 CMOSN
M3 2 2 3 0 CMOSN
M4 4 2 5 0 CMOSN 
* analysis requests
.dc vo 0V 25V 10mV
.control
run
* output requests
plot -i(vo)
plot v(2)-v(4) v(3)-v(5)
.endc
```

![Screenshot from 2022-07-12 18-08-14](https://user-images.githubusercontent.com/68816726/178466671-5a01b6a9-c66d-4f34-bdb9-34ea80f7855d.png)
