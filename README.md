# Lte_RRC_meas
My lte-RRC measurement project RRC_MEASUREMENT v8.4.0
﻿/*please see second change*/ //This change is not acceptable
/********************************************************************************************************************************** 
All rights reserved – Nex-G Exuberant Solutions Private Limited.                                                              **** 
File Name    : Readme_RRC_MEASUREMENT.txt                                                                                     **** 
Module Name  : RRC_MEASUREMENT                                                                                                **** 
Project Name : RRC_MEASUREMENT v8.4.0                                                                                         **** 
Description  : Readme file for RRC_MEASUREMENT                                                                               **** 
Author       : Manu Deva Arya, Gyanendra, VirenU.                                                                             **** 
Start date   : 18-04-2017                                                                                                     **** 
End date     : 30-04-2017                                                                                                     ****
***********************************************************************************************************************************/

-------------------------||        Release  3GPP TS 36.331 version 8.4.0 Release 8         ||--------------------------------------

The functional entities of the RRC layer are described below:

1) Routing of higher layer messages to different MM/CM entities (UE side) or different core network domains
   (UTRAN side) is handled by the Routing Function Entity.

2) Broadcast functions are handled in the broadcast control function entity (BCFE). The BCFE is used to deliver
   the RRC services, which are required at the GC-SAP.
   The BCFE can use the lower layer services provided by the Tr-SAP and UM-SAP.

3) Paging of UEs that do not have an RRC connection is controlled by the paging and notification control function
   entity (PNFE).
   The PNFE is used to deliver the RRC services that are required at the Nt-SAP.
   The PNFE can use the lower layer services provided by the Tr-SAP and UM-SAP.

4) The Dedicated Control Function Entity (DCFE) handles all functions specific to one UE.
   The DCFE is used to deliver the RRC services that are required at the DC-SAP and can use lower layer services of UM/AM-SAP and
   Tr-SAP depending on the message 
    to be sent and on the current UE service state.

5) To execute this project we'll use Shared Memory for receiving command from EUTRAN and Message Queue for sending Measurement data.

6) In 3GPP_rrc_measurement_rel8.4 there are all the files main_ue.c, main_eutran.c, makefile, main_wrapper.h, main_linkedlist.h,     
   MAIN_MACROS.h, MAIN_HEADERS.h, MAIN_IPC.h, MeasConfig.h, VarMeasConfig.h
   
7) In RRC_Measurement all these module run one by one means in specific order which we called function it will execute.


----------------------------------------------------\      STEP-1     \------------------------------------------------------------------

a) for first module MeasConfig.h structure fetched from lte_asn.1

b) At EUTRAN side fetched all nested structure for IEs  of MeasConfig.h such as MeasObjectTORemoveList, MeasObjectToAddModList,
   ReportConfigToRemoveList, ReportConfigToAddModList, MeasIdToRemoveList, MeasIDToAddModList etc.

c) There are modules of different Measurement for that we have declared functions respectively in  main_eutran.c

d) All header files are inclued in main_headers.h 

e) Now we have created the shared memory for both the  UE and EUTRAN side.

f) shared memory created by shmget function for sending command to EUTRAN from UE.


---------------------------------------------------\       STEP-2     \------------------------------------------------------------------

h) for second module VarMeasConfig.h structure fetched from lte_asn.1

i) At UE side fetched all nested structure for IEs  of VarMeasConfig.h such as MeasObjectToAddModList, ReportConfigToAddModList,
   MeasIDToAddModList etc.
a) There are modules of different Measurement for that we have declared functions respectively in  main_ue.c

b) All header files are inclued in main_headers.h 

e) Now we have created the Message Queue for both the  UE and EUTRAN side.

g) after that used msgsnd and msgrcv function for communication between UE and UTRAN i.e, Measurement reporting to  EUTRAN.



----------------------------------------------------\       STEP-3     \----------------------------------------------------------------


h) EUTRAN send Command by memcpy function through shared memory, inrespect of EUTRAN_CMD, UE performs the measurement and send meas_report
   through Message Queue.

i) The meas_report send to EUTRAN  by CCCH channel.

j) The meas_control_cmd receive form EUTRAN through BCCH channel.


---------------------------------------------------\       STEP-4     \-----------------------------------------------------------------

k) EUTRAN receive meas_report of UE from mssgsndand msgrcv function.

l) Through printf function printed the meas_ at UTRAN side.


----------------------------------------------------\       STEP-5     \---------------------------------------------------------------

m) At the execution of program first we compile main_eutran.c and main_ue.c.

n) EUTRAN side & UE side module creating executable file eutran_side & ue_side with the help of makefile.

o) Then we exucute from executable file for sending CMD(eutran_side) and Receiving CMD(ue_side) in EUTRAN and UE side Respectively. 

p) When all the process has been completed the data with the help of message queue send further to next module.

q) After that it's also checked with valgrind to check memory leakage.

r) But we did not find any leakage.

s) All the data which received or send in during execution stored in logfiles.

t) All the message queue has been also deleted after completion of every module.


------------------------------------------------------------------\   \-----------------------------------------------------------------




********************************************************************************************************************************************************************

        						End of file readme.txt

**********************************************************************************************************************************************************************/
	
