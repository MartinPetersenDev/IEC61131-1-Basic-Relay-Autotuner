# IEC61131-1-Basic-Relay-Autotuner
Basic Relay Autotuner for IEC 61131-1 languages

AUTHOR:
Martin Petersen (http://firmaetpetersen.dk)

VERSION: 
1.0	05-06-2018	Initial version
1.1	17-08-2018	Added parameters for setting minimum change in proces variable (MinChangePct), number of tuning cycles (NoCycles [1-10]) and functionality to remove max and min measurement outliers before calculating parameters (RemoveOutliers).

GENERAL INFORMATION:
This is an IEC 61131-1 implementation for a relay based autotuner. It's purpose is to be highly portable between PLC's,
thus it is a very general implementation, and requires the use of surrounding logic when implemented.

The tuner manipulates the proces and calculates the proces ultimate gain and period. These values can be used to calculate
PID parameters with the suggested values below.

The calculation parameters are designed for the ideal PID algorithm 
	OUTPUT = Kc * ( e(t) + 1/Ti integral_e(t) d t + Td*e'(t) )

BASIC USAGE:

1)	Configure StepChange, InputMin, InputMax and PID_Output.
2)	Optionally configure MinChangePct, NoCycles and RemoveOutliers.
3)	Connect the program to ProcesInput and ControlOutput.
4)	Run the plant at a realistic operating point, and wait for a steady state process (THIS IS VERY IMPORTANT)!
5)	Put the PID controller in manual mode.
6)	Start the tuner with TunerStart=TRUE.
7)	When the program finishes, the outputs Kc and Pu can be used to calculate PID parameters. An optional DeadTime is also measured, but only make the user aware of the relation between deadtime and the proces period.
8)	Calculate the new PID parameters.
9)	Disable the tuner with TunerStart=FALSE.
10)	Put the PID controller in auto mode.
11)	Sometimes the proces will achieve a better steady state after tuning, and a new tuning can be done.

Suggested PID parameters:

Original ZN, Kc=0,6*Ku Ti=Pu/2 Td=Pu/8

Little Overshoot, Kc=0,33*Ku Ti=Pu/2 Td=Pu/3

No overshoot, Kc=0,2*Ku, Ti=Pu/2, Td=Pu/3

Suggested PI parameters:

Original ZN, Kc=0,45*Ku Ti=Pu/1,2	

Little Overshoot, Kc=0,25*Ku Ti=Pu/1,2	

No overshoot, Kc=0,15*Ku Ti=Pu/1,2


