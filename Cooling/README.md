This project implements the cooling power system for Columbia FSAE Electric. 
The goal is to power and independently control multiple high-current cooling loads using the battery voltage, which ranges from approximately 360 V to 600 V.



From the tractive battery, the system needs to:

1. Supply two Tractive Battery Pack (TBP) fans. Each fan requires about 4.7 A at 24 V with up to 5 A inrush. Total requirement is about 10 A at 24 V.

2. Supply two radiator fans. Each requires about 2.4 A at 24 V with about 2.7 A inrush. Total requirement is about 4.4 A at 24 V.

3. Supply the cooling pump which requires 13 A at 12 V.

4. Allow independent control of each cooling device.


Solution Overview:

<img width="1920" height="1080" alt="Block Diagram copy" src="https://github.com/user-attachments/assets/dc0a4bdb-a9b8-49dc-a875-ae89454b8a18" />

The system uses two PicoDCA-24S isolated DC-DC converters which convert approximately 300–700 V tractive voltage to 24 V at 12.5 A.

The first PicoDCA-24S supplies the TBP cooling fans. Its 24 V output is fed through a high-side smart switch (VN5T016AHTR-E), which provides switching control, protection, and current monitoring.

The second PicoDCA-24S supplies both the radiator fans and the cooling pump. Its 24 V output is split into two branches:

One branch powers the radiator fans through another VN5T016AHTR-E high-side switch for control and protection.

The second branch feeds a buck converter (QHHD019A0B41-HZ) that converts 24 V to 12 V. This 12 V rail powers the cooling pump, again with switching and current monitoring capability.

Each load can be controlled independently, controled by signals recived from the MCU. The system is protected with fuses, TVS devices, and the protection features of the smart switches. The converters provide high voltage isolation and are designed to handle the inrush currents and continuous current demands of all cooling components.
