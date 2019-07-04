# MakPrint v1.1

hi guys and thankyou for downloading MakPrint v0.1 Firmware

i want to make MakPrint "THE" Go-To Easy to install Firmware for all these chinese printers and with your help i hope to make this happen

---------------------------------------------------------------------------------------------------------------------------------------------
 please note.. if 'you' kill your printer.. then let it be known that ''YOU'' killed it .. not me.
 
follow these instructions and you should end up with a working MakPrint V0.1 (marlin) firmware with 9 point autobed leveling

i must have a slightly warped bed on my printer because for some reason the repetier firmware with its 3 point leveling would only work for 
small parts located in the center of the bed.. i tried adjusting the firmware to allow for grid bed leveling but couldnt get it to use the
co ordinates i had set.. marlin works for me so im happy and hopefully itll work for you too.. 
i printed the same large part which spans the whole bed on repetier and on MakPrint V0.1 and on repetier well.. it didnt work.. i had my nozzle
gouge out scratches on both sides of the bed... i switched over to this and printed the same part with the same offset settings and it just worked
 so like i said.. im very happy ..

------------------------------------------------------------------------------------------------------------------------------------------------------
Changelog;
V0.1 First Version.
v1.1 Updated Loading Screen.

Up Comming Versions;
v1.2

-----------------------------------------------------------------------------------------------------------------------------------------------------------

to install firmware

1. unzip all files
2. open arduino 1.6.3
3. go to 'Tools' then 'Board' and make sure 'Anet v1.0 is selected
4. underneath 'Board' go to 'port' and set the required com port for your printer -eg. COM4 etc
5. click File -Open - and navigate to the MakPrint V1.1 folder and open MakPrint_V1.1.ino
6.click upload and wait..
7. when your printer reads MakPrint on the screen your done and it is installed
-----------------------------------------------------------------------------------------------------------------------------------------------------------
we will now set up the offset because once the printer homes to z - the nozzle wont be close enough to the bed! 
i use cura 3.0 or pronterface for this.
and for normal SD Prints i use PrusaSlicer.

1.so install that. go to preferences and set print window to pronterface ui
	set up your machine settings and make sure the com port and baudrate match your printer
2.load up any stl model and hit print... we wont actually be printing right now so dont worry too much here about the settings
3.manually control with the buttons in the print window so that the nozzle is just touching the build plate
4. adjust your sensor so that it is about 1mm above the build surface when the nozzle just touches
5. raise z by 10 (tool up button) 
6.press the white 'home' button
7. slide a piece of paper underneath you nozzle
8. type G92 Z10 and hit enter- to check this command has worked type M114 and you should get a line similar to  this with Z:10.000

 	(X:131.00 Y:153.00 Z:10.00 E:0.00 Count X: 131.00 Y:153.00 Z:10.00)

9. lower the nozzle using the 0.1down button until theres a little bit of friction on the paper (like you would if your were leveling normally)
10. type M114 and you should get a line like this where z is lower than 10.000

	(X:131.00 Y:153.00 Z:8.90 E:0.00 Count X: 131.00 Y:153.00 Z:8.90)
	
you see mine is  "Z:8.90"

11. get your scientific calculator out and punch in the numbers 10-Z (z being the number you just got from lowering the nozzle) 
12. that is your offset... or damn near close.. you can adjust it finer by playing about .. but thats pretty much it...

mine was 1.1.. add a minus and a couple of m's and you get -1.1mm << that is your offset for the next part
-------------------------------------------------------------------------------------------------------------------------------------------------------------
now we will reconfigure the firmware to have the correct offset value

1. open arduino
2. click File -Open - and navigate to the MakPrint_V0.1 folder and open MakPrint_v0.1.ino
3. go to the 'configuration.h' tab 
4. hit ctrl+f and copy this line below into find

#define Z_PROBE_OFFSET_FROM_EXTRUDER 		0//-12.35

5.change the 'zero' so it reads your offset figure (-1.1mm)

#define Z_PROBE_OFFSET_FROM_EXTRUDER 		-1.1//-12.35
	
6.click upload and wait..
7. when your printer reads MakPrint on the screen your done and it is installed...again.. only with the offset being correct this time :)

-------------------------------------------------------------------------------------------------------------------------------------------------------------

now just add a G29 after the G28 
