# clkbrd3
In 2021, even 32kHz oscillators are hard to come by!  
# Motivation
I built this board due to parts shortage and cost issues.  My friends at SiTime are quoting **86 week leadtime** for SiT1532 32.768kHz MEMS oscillators as of the end of July 2021 .  
Diodes KX321 32.768kHz crystal oscillators are available from DigiKey, albeit at $1.83 per unit in 1k quantities.  
The design objective for clkbrd3 was a very low-power, very low-cost crystal oscillator with a minimum of board area so it could be used in "always on" consumer electronics.  The circuit is from The Art of Electronics 3rd Edition by Horowitz & Hill, Section 7.1 figure 7-40.  U2 is in the Pierce configuration and has 10k resistors on power and ground to reduce cross conduction current.  U4 schmitt trigger inverter cleans up the signal and U5 amplifies it to 1.8V (or 2.5V or 3.3V) LVCMOS levels.  See H&H for more deails.  
# Results
Fabricated at [JLCPCB](URL "https://jlcpcb.com") July, 2021.  I originally tried LVC logic components because they were cheaper but they don't work below 1.65V and the current consumption was way too high.  
## Power 
I measured current consumption with a Keysight B2901A SMU. With AUP devices installed, I did measure higher current than what H&H quoted: 867nA for 0.9V 1st stage, and 4.54uA for 1.8V w output driver for a total power consumption of 8.95uW.  I have not investigated the reason for the discrepancy.  Jitter performance is quite good, peak-to-peak jitter of around 3ns.  
## Cost
Nexperia raised prices on the AUP devices after I bought them.  

Designator  | Description | Component | Cost 1k qty
------------ | -------------| ------------- | -------------
U4 | Schmitt Trigger Inv |SN74AUP1G14DCKR | $0.066
U2 | Unbuffered inverter | 74AUP1GU04GW,125 | $0.1059
U5 | Buffered inverter | SN74AUP1G04DCKR | $0.072
Y1 | through-hole xtal | TDXLF-206 32.768 | 0.0481
C5 | 0.1uF cap X7R 0402 | CC0402KRX7R9BB104 | $0.0031            
C8 | 0.1uF cap X7R 0402 | CC0402KRX7R9BB104| $0.0031
C10 | 0.1uF cap X7R 0402| CC0402KRX7R9BB104| $0.0031
C9 | 10n cap X7R 0402   | CGA2B2X7R1E103KT0Y0F | $0.0069
R4 | 10M ohm 0402 | 0402WGF1005TCE | $0.0007
R5 | 330k ohm 0402 | 0402WGJ0334TCE | $0.0005
C4 | 22pF 0402 C0G | CC0402JRNPO9BN220 | $0.001
C6 | 22pF 0402 C0G | CC0402JRNPO9BN220 | $0.001
R7 | 10M ohm 0402| 0402WGF1005TCE | $0.0007
R3 | 10kOhm resistor,0402| RC0603FR-0710KL | $0.0012
R2 | 10kOhm resistor,0402| RC0603FR-0710KL | $0.0012

for a total BOM for the oscillator of $0.3155.  The price increased 8 cents from when I bought the parts in early July.  
Who says there is no inflation?
## Area
The actual oscillator area is 8mm x 8.3 mm, using a 4 layer stackup with signals and components placed on top and bottom.  Smaller packages would make the area much smaller but carry a cost adder.  A rant on 4-layer boards.  The JLCPCB boards were $2 for 5 boards?  Why would anyone build 2 layer boards at that price?
# Instructions
## To Edit
To edit the schematic or layout, or use in your own projects, clone the repo.  
note that KiCAD 5 gets confused, I think because of the 10k resistors on power nets.  If you look at the layout there appears to be a problem but I just ignored it and fabbe the board and it worked fine.
## To Build
To just build it as-is, use the zip file in ./gerbers and upload it to jlcpcb.
# Operation
Board is a low current consumption 32kHz crystal oscillator evaluation board.  see the schematic in the ./schematic directory.  For convenience, can be powered by a 5V USB Micro connector or a 5V barrel jack.  U1 and U3 are LDOs, not low-power, low-Iq or cheap, but convenient.  RV1 and RV2 are potentiometers to set the voltage for VXTAL and VDDIO.  
J3 selects whether to use a 5V barrel jack (J3 == 2-3) or micro USB (J3 == 2-1).  Adjust RV1 to provide 1.8V on VDDIO (J5 pin 1) and adjust RV2 to provide 0.9V on J8.1.  32kHz clock output is available on J6.1 or J7 SMA connector, if installed.  
# Conclusion
You can build a low-power 32kHz oscillator out of discrete components for much less than the cost of a crystal oscillator.  Performance is good, as long as the startup time is not critical.
