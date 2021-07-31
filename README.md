# clkbrd3
In 2021, even 32kHz oscillators are hard to come by!  
My friends at SiTime are quoting **86 week leadtime** for SiT1532 MEMS oscillators as of the end of July 2021 .  
Diodes KX321 are available from DigiKey, albeit at $1.83 per unit in 1k quantities.  
So, I designed a PCB for a 32kHz Low power crystal oscillator using 74AUP logic.  The circuit is from The Art of Electronics 3rd Edition by Horowitz & Hill, Section 7.1 figure 7-40.  
I designed this PCB to be as small as possible (the actual oscillator circuit measures 8mm x 6mm of board space), and to be as inexpensive as possible. 
Fabricated at [JLCPCB](URL "https://jlcpcb.com")July, 2021
Note that I measured substantially higher current than H&H quoted: 867nA for 0.9V 1st stage, and 4.54uA for 1.8V with an *AUP1GU04* output driver.  I didn't have any AUP1G04 lying around.  Measured with a Keysight B2901A SMU.  Jitter performance is quite good, peak-to-peak jitter of around 3ns.  Overall I am happy with this implementation.
