## Generating Gerber (CAM) Files 
Most PCB fabrication shops use Gerber files, which are a vector-image format of the various circuit board layers required for manufacture.

[Alberta Printed Circuits](http://apcircuits.com) accepts this format (Gerber RS274X specifically), along with Excellon-formatted drill files, which are essentially an M-code program for drilling the holes in the PCB on a CNC machine.

The procedure for doing this in '''EAGLE 6''' is as follows:
* Have the desired project open. It is good practice to run DRC/ERC checks before generating CAM files to catch any layout errors.
* Open the CAM Processor (File->CAM Processor)
* Open the Job file (apcircuits.cam) for APC (File->Open->Job)
* Confirm each individual Gerber file (represented by the tabs) contains the necessary layers.
* Confirm the 'Drill File' tab has 'Excellon' selected for Device, and the Rack file is the apcircuits.drl file.
* Click 'Process Job'

If the CAM Processor indicates a hole size error, it may be necessary to adjust the 'Tolerance' option in 'Drill File'. It's best to leave the minus tolerance at 5% (although 7% can be used in a pinch). Increasing the plus tolerance is a better choice in most cases.

## Gerber Files and Layers 
Gerber files should contain the following layers at a minimum (note that the apcircuits.cam file generates them this way by default):
* Top Copper (.GTL) - Top, Pads, Vias, Dimension
* Bottom Copper (.GBL) - Bottom, Pads, Vias
* Top Silkscreen (.GTO) - tPlace, tNames, tValues
* Bottom Silkscreen (.GBO) - bPlace, bNames, bValues
* Top Soldermask (.GTS) - tStop
* Bottom Soldermask (.GBS) - bStop
* Drill File (.TXT) - No layers, technically not a Gerber file

Some Notes:

* Since bottom silkscreen costs extra from APC, it is often not included (or required). 
* The 'Dimension' layer doesn't HAVE to be in the Top Copper layer, but it should be included in one of the layers to show the overall dimensions of the board.
* [Gerbv](http://gerbv.sourceforge.net) is a free Gerber File Viewer that allows you to view the layers and drill file together to get an idea of the final product. This can be useful for catching errors in copper or silkscreen before sending to fabrication.

## Submitting to APC

Submit files online [HERE](https://www.apcircuits.com/ap/webclient)

Use the Prototype Plus, FR4 substrate, 1oz. Copper (fairly standard for consumer PCBs). 

Hole sizes generated are '''actual tool diameter''', be sure to specify that in the order.

Ensure you include GTL, GBL, GTO, GTS, GBS and TXT files (6 files).

Submit design well before 11am to get it into the production queue for the same day.

