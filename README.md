# twl_firm_patcher

This patcher that allows to produce a special twlBg.cxi by patching the devLauncher SRL contained into it.

This modifed twlBg.cxi allows to unlock the TWL mode Hardware (DSI) into the NTR mode (DS)

This unlock new capabilitys in NTR mode without breaking games:
-  boost arm9 speed (from 66 mhz to 133 mhz)

Usage :
- Dump the twl_firm of your console using decrypt9 (SysNAND Options->Miscellanous->NCCH FIRMs Dump)
- rename it to firmware_twl.bin and put it into input.
- run go.cmd
- put the twlBg.cxi file into luma/sysmodules (V6.0 dev version required)
- an "enabler" program is needed to unlock the HW. 

Here are some example of enabler programs : 
- https://github.com/ahezard/ntr_extended__poc
- https://github.com/ahezard/woodrpg_forwarder

Limitation : only the arm9 is unlocked, the arm7 appears to be still locked in NTR mode

Here are the details of the patches implemented :

The idea is to replace all STR operations on the register 0x4004008 by STRH (only affect bit 1-16 leaving bit 16-32 untouched)

In devLauncher SRL :

ARM9 section (0x004000-0x02A000)
- offset 0x07368 replace 08 60 87 05 by B8 60 C7 01 

ARM7 section (0x02A000-0x034888)

ARM9i section (0x055C00-0x059C00)

ARM7i section (0x059C00-0x05F550)
- offset OxA5888 replace 00 00 85 E5 by B0 00 C5 E1

All of this started from a Normatt theory so special thanks to him for the idea behind :
- [9:26:23 PM] Normmatt: 4004008h - DSi9 - SCFG_EXT - Extended Features (R/W) [8307F100h]
- [9:26:32 PM] Normmatt: just make sure bit31 is NEVER set
- [9:26:42 PM] Normmatt: and boom you can re-enable all twl hardware from ntr mode

Thanks again to Normatt for the ARM7 patch.

Thanks as well to Apache Thunder and Shutterbug2000 for the testing and hacking support.
 