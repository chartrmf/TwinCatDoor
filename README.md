# TwinCatDoor
TwinCat version that should be loaded into PLC for door control

TwinCAT 3.0
The TwinCAT solution file, that runs on the PLC, opens and closes the door according to its logic and the status of the specific OPC variables. These variables are hosted on the internal OPC server and exposed to any other OPC client to read and write. In this package, the ROS package is the OPC client while the PLC hosts the OPC server.

Port on PLC	OPC Variable (Boolean)	Description
N.A	chart_cssd_door_Status	Status of door. Opened = True. Closed = False
KL 2622 (B) CH1	chart_cssd_door_Contact	Status of door contact. Energized = True. De-energized = False
N.A	chart_cssd_door_Open_Command	Command from OPC client to send door open command.
N.A	chart_cssd_door_Close_Command	Command from OPC client to send door close command.
KL 1184 (B) CH1	chart_cssd_door_Opened_Signal	Signal when door is fully opened.
KL 1184 (A) CH1	chart_cssd_door_Closed_Signal	Signal when door is fully closed.
KL 2622 (A) CH1	chart_cssd_door_Hold	Signal when door is held open

According to the internal logic of the TwinCAT program, the door will be opened (and held in the opened position) depending on the status of the relevant variables. 

The truth table below shows the output of door open and door hold according to the status of various inputs. It gives a quick overview of how the internal logic of the PLC software works. Only when the door open command and the door close command are in its desired values, can the door be opened via the door hold and door contact variables. The door hold and door contact variables are directly wired to the PLC card for activation of the door contacts. 

Input	Output
chart_cssd_door_Open_Command	chart_cssd_door_Close_Command	chart_cssd_door_Hold	chart_cssd_door_Contact
1	1	0	0
1	0	1	1
0	1	0	0
0	0	0	0

