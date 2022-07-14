# SPICE-Amplifier
## Current Mirror-BJT

* 電流鏡是一種常見的IC 設計技術。在這種技術中，電路的設計方式是將一個主動元件的電流複製到另一個具有電流控制功能的主動元件。在這種情況下，流過一個元件的電流可以被複製到另一個元件中
* 如果前面的電流發生變化，另一個元件的鏡像電流輸出也會發生變化。
* 因此，通過控制一個設備中的電流，也可以控制另一個設備中的電流。
* 電流鏡電路通常被稱為電流控制電流源或 CCCS。

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


# Common Gate

![Screenshot from 2022-07-14 21-21-13](https://user-images.githubusercontent.com/68816726/178992250-51a61c60-5661-4629-897d-4843f1913391.png)

netlist
```
High-Frequency Response of Common-Gate Amplifier
* circuit description *
Vdd 4 0 +20V
Vin 1 0 dc 0 ac 1
R 1 2 100k
Rg1 4 3 1.4Meg
Rg2 3 0 0.6Meg
Rd 4 5 5k
Rs 6 0 3.5k
Cs 6 0 1u
Cc1 2 3 1u
Cc2 5 7 1u
Rl 7 0 10k
* model description *
M1 5 3 6 0 mosfet L=1u W=64u
.model mosfet nmos (kp=100u Vto=1V lambda=0 CGSO=15.625n CGDO=15.625n)
* analysis requests *
.ac dec 100 10kHz 1GHz
.control
run
plot db(v(7))
.endc
```

![Screenshot from 2022-07-14 21-20-01](https://user-images.githubusercontent.com/68816726/178992342-7a6bc4da-14f3-4c6b-9822-ad38055e7190.png)

# Common source

![Screenshot from 2022-07-14 21-24-30](https://user-images.githubusercontent.com/68816726/178992858-b1ade4c8-00c4-4a91-a733-e9eb679a4646.png)

netlist
```
Low-Frequency Response of Common-Source Amplifier
* circuit description
Vdd 4 0 +20V
vi 1 0 ac 1 
R 1 2 100k
Rg1 4 3 1.4Meg
Rg2 3 0 0.6Meg
Rd 4 5 5k
Rs 6 0 3.5k
Cs 6 0 1u
Cc1 2 3 1u
Cc2 5 7 1u
Rl 7 0 10k
* model description
M1 5 3 6 0 mosfet L=1u W=64u
.model mosfet nmos (kp=100u Vto=1V lambda=0)
* analysis requests
.ac DEC 10 1Hz 10kHz
.control
run
plot db(v(7))
.endc
```

![Screenshot from 2022-07-14 21-23-38](https://user-images.githubusercontent.com/68816726/178992975-2bd1b2ad-903f-4ebc-80eb-1aac9b868e58.png)
