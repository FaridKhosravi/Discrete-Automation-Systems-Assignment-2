# Discrete-Automation-Systems-Assignment-2

Objective:
The second assignment objective is to use different methodologies to represent the problem and then solve it in PLC programs using Beckhoff TwinCAT.

The problem should be solved with both state chart and flowchart methodologies - so, there are two programs to write using each of the methodologies.

Task - Reference system:
The system is composed of a conveyor loop and three workstations joined with it. The conveyor is used to deliver pallets to the workstations. The pallet is introduced to the system at WS1, then each pallet must visit WS2 and WS3. The pallet that has visited all the workstations is removed from the system at the WS1. Each workstation can process 1 pallet at the time. It takes 5 seconds for a workstation to process the pallet. If the workstation is busy processing the pallet and a new pallet comes to its location needing also the service of that particular workstation, then that new pallet continue on the conveyor loop to come to the workstation on the next cycle - as it circulates the conveyor belt to appear in front of that workstation again. It is does not matter in which order the WS are visited - important is that all of them will be visited. The conveyor can be seen as a dynamic buffer that can have pallets circulating until a pallet has visited all the workstations.

Outputs:
1)Motor - the motor to control the conveyor. (BOOL) In general should be always on, as the pallets are stopped by the stoppers at the WS.
2)Stoppers S1..3 - to stop a pallet at the corresponding workstation. (BOOL)
3)Board available BA1..3 - to signal to the corresponding workstation that the pallet has arrived. (BOOL)

Inputs:
1)Locked by WS L1..L3 - WS signals that it already has the pallet for the processing. (BOOL)
2)Presence sensors P1..3 - sensors telling that there is a pallet in the corresponding location in front of a WS. (BOOL)
3)Pallet_in - A button to introduce a pallet to the system at WS1 position.

With respect to BAx and Lx signals the logic can look as follows: A pallet arrives at WSx, the program checks Lx. a) If Lx is true the pallet continues by the conveyor to the next WS. b) If Lx is false and the pallet needs the service of that WS, then BAx signal goes on. The BAx signal should go off once Lx goes on, which means that the WSx has taken the pallet. The pallet is then in the WSx (for 5 seconds). Other pallets can bypass the WSx holding a pallet. Then, after the processing, the pallet should be returned to the conveyor belt and Lx goes off. (The pallet can be returned from the WS to the conveyor belt, if and as there is no any other pallet - Px and BAx inputs are off.) 

You will also have to implement some memory structure monitoring if the pallet was tended at all the workstations.
