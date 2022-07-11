# SPICE-BJT
## Current Mirror

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
