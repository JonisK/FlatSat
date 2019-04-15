The PC/104 FlatSat used for the development and testing of the CubeSat [MOVE-II](https://www.move2space.de/MOVE-II/)

FlatSat
===

The FlatSat is a test environment aimed at developing and verifying interactions between all subsystems of a CubeSat based on the PC/104 bus. The FlatSat consists of two large PCBs which have PC/104 sockets for plugging in all subsystems. The flat assembly makes probing the subsystems easier and reduces wear on the PC/104 connectors of the subsystems.

![](https://i.imgur.com/MPITqvF.png)

# Mechanical Characteristics
The FlatSat rests on a base made of aluminium profiles with aluminum sheets on top. Every subsystem has one aluminium sheet that can be customized to have threaded holes below the mounting holes of the subsystem board. Standoffs can then support the subsystem board mechanically and also connect the subsystem to the structure electrically as pointed out in section X. Atop the layer of aluminium subsystem sheets, another aluminium sheet for supporting the FlatSat PCBs is placed. A plastic sheet between that backbone and the FlatSat PCBs prevents short-circuits.
![](https://i.imgur.com/2aEkqMM.png)

![](https://i.imgur.com/NRY2BVD.jpg)

![](https://i.imgur.com/inGY6t5.jpg)

![](https://i.imgur.com/pjFeFbK.png)

![](https://i.imgur.com/WgzFMks.jpg)

Two large PCBs with three PC/104 connectors on the sides, one in the front, and one in the rear are assembled in line with each other to form the electrical connection of the FlatSat. The front and rear connectors in the middle are connected with the PC/104 bridge board documented in section X. In total, the FlatSat has six connectors on the long sides and one in the rear for subsystems of MOVE-II.



Each PC/104 connector on the long sides of the FlatSat board is spaced 120mm center-to-center from the next one. The subsystem boards may be up to 100mm wide. For the CDH board, the maximum width is 160mm, since an early development board used for the MOVE-II project was quite a bit larger than the typical 90*95mm PC/104 footprint. The width for the ADCS is even larger since the Sidepanels also need to fit around the Mainpanel. The rear PC/104 connector could fit an infinitely wide board. The front PC/104 connector has the exact same orientation as the rear PC/104 connector so it cannot be used for mounting a subsystem but is solely for monitoring the bus over the PC/104 breakout board or connecting multiple FlatSat boards with a PC/104 bridge board.

# Signal Integrity
The long and branched traces in the FlatSat PCB deteriorate the signal quality significantly in comparison to the PC/104 bus built from the subsystems in the final stacked configuration. SPI communication at 5 MHz between the CDH and S-Band, at 4 MHz between CDH and ADCS, at 1 MHz between CDH and UHF/VHF, and at 4 MHz between the CDH and the PL (Toppanel) worked flawlessly. Also, the I²C communication between CDH and EPS at 400 kHz suffered no issues. An oscilloscope measurement shown in figure X depicts how the edges of the SPI signals deteriorate at 5 MHz. The probes were placed on the Monitor PC/104 connector. Only the internal ADCS bus connecting the Mainpanel to the Toppanel cannot operate at the full frequency due to 3.9 kOhm inline resistors on the Toppanel Adapterboard. The ADCS firmware needs to be reflashed with a version using 400 kHz instead of 4 MHz for the internal buses while the ADCS is on the FlatSat.
![](https://i.imgur.com/4gzIgyG.jpg)
Some of the PC/104 pins are used for carrying supply currents in MOVE-II, so their traces are wider. The SPI pins H1-47, H1-49, and H1-51 are broken out to through-hole pads at each connector for proper termination. Since testing showed acceptable signal integrity, none of the termination pads were populated with resistors.
Every communication pin at every connector is routed through a 0603 0 Ohm resistor that can be substituted with resistors of higher value to simulate the behavior of a bus that has suffered from fretting corrosion. This possibility was not utilized during MOVE-II testing.

# Grounding Concept
Tha FlatSat tries to resemble the conductance characteristics of the real MOVE-II satellite. All parts of the structure have low-impedance connections to each other and the FlatSat does not connect any PC/104 pins to the structure.
Hence the grounding of the structure must be done by one of the subsystems, in case of MOVE-II the EPS battery board.
The FlatSat structure rests on anodized aluminium profiles making it isolated from the desk it is sitting on. In the MOVE-II integration room, the FlatSat rests on a grounded stainless steel desk so the isolation of the aluminium profiles allows us to control the impedance between the FlatSat structure and Earth potential. A separate wire connects the FlatSat structure to the grounding bus in the integration room which connects to Earth over a 100 kOhm resistor.

# Use in MOVE-II
The FlatSat was finished in December 2016. Its utilization within the MOVE project began in January 2017 with the brass prototypes that the team developed until the X-mas milestone. After a few tests in teh student lab shown in figure X, the FlatSat was put in the integration room of LRT next to a PC that connects to the UART console of the CDH on the FlatSat. 
![](https://i.imgur.com/lrOh7D5.jpg)

Connecting a new subsystem revealed a lot of bugs associated to communication with the CDH or receiving power from the EPS. The FlatSat then provided easy access to debug connectors and test points supporting the developers in fixing the found bugs. In March 2017, all subsystems were connected to the FlatSat for the first time. Further milestones were the 24 hour test and the first LEOP tests that showed correct actuation of the deployment mechanism. By cutting traces on the PC/104 bridge and replacing them with a currentmeter, the power demands of every subsystem were measured. In May, after transitioning to testing in the fully integrated configuration, the FlatSat was not the focal point of the team's debugging effort anymore but was used regularly whenever a new hardware incarnation, like the FM and the FMb, was tested. After more than two years of use, the FlatSat is still in good shape and shows no significant mechanical or electrical wear. 
![](https://i.imgur.com/p34K63L.jpg)

# Adaptability to new missions
The FlatSat PCB Altium project is uploaded in the github repository MOVE-II FlatSat and may be utilized, and modified in accordance with the MIT license.
The mechanical assembly can be found in the same repository in Autodesk Inventor's .iam format.
The spacing between the PC/104 connectors can easily be adjusted for wider boards. The smallest center-to-center distance between two subsystems needs to be at least 120mm because of the width of the traces needed for routing the bus to the connector.
The PCBs can be made longer to fit more PC/104 connectors or more of the PCBs can be made and connected via the bridge board to allow for more connections. Refer to the maximum board length your PCB manufacturer allows. The limit typically is 400mm.
The trace-widths and termination breakouts described in section X can be adapted to different projects.
If the new mission uses a bus with more or fewer pins on the connector, adapting the FlatSat PCB might not be reasonable.

# Bill of Materials
Number 	Name 	Description
20 	Samtec SSW-126-01-G-D 	For 10 PC/104 sockets
1 	PCB 263x100mm 	Rear half (UKW, Reserve, EPS, Toppanel)
1 	PCB 294x100mm 	Front half (Monitor, ADCS, S-Band, CDH)
2 	SMT S1084040L 	Aluminium profile 40x40x300 leicht
2 	SMT S1084040L 	Aluminium profile 40x40x700 leicht
1 	SMT S1084040L 	Aluminium profile 40x40x370 leicht
1 	Aluminium sheet 560x100x3mm 	Backbone to support the PCBs
1 	Plastic sheet 560x100x2mm 	Spacer between PCBs and backbone for isolation
1 	Aluminium sheet 506x20x3mm 	Spacer between profiles and backbone

