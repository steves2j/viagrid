# Viagrid

Viagrid is a PCB template standard that allows for rapid PCB prototyping with 2-layer boards and factory vias.

When doing board layout, you drop your components onto the Viagrid template file. This shows you where the Viagrid blank already has vias embedded. When routing your board, simply drop your vias only where the Viagrid blank already has them.

When it comes time to fabricate your board, all that needs to happen is remove copper from the top and bottom layers, effectively deciding which net the vias are part of. This process can be done using acid etching, UV DPSS lasers, or CNC machining.

!!! "Compatible Software"
    Viagrid supports only KiCAD by default at the moment.

## File Prep

### Design

1. Design your schematic in KiCAD like you usually would. Assign footprints.
2. Before opening the .kicad_pcb file associated with your project, copy the `viagrid-template.kicad_pcb` file into your KiCAD project directory, and rename it to replace the default one.
3. Open the newly renamed `.kicad_pcb` file in KiCAD. The `User1` layer shows the location of the vias on the Viagrid blank, and the outer bounds of the usable area.
4. Set your board settings for best results:
   1. Vias: 1.5mm ring, 0.3mm drill
   2. Traces: no smaller than 0.2mm
   3. Copper pour: at least 0.3mm clearance
5. Route your board like you normally would.

### Export

1. File -> Plot
2. When exporting, we only care about the front and back copper layers, and the front and back mask layers. Select these.
3. Export files as .DXF

## Fabrication

### UV DPSS Method

Viagrid boards can be easily and autonomously cut using a UV DPSS (Diode Pumped Solid State) laser. These are commercially available and getting cheaper by the year. These instructions were prepared using a [Commarker Omni 1 (5W)](https://store.commarker.com/products/omni-1-uv-laser-engraver) however the same company has recently released a similar machine that is fully enclosed, called the [Omni X](https://store.commarker.com/products/omni-x-uv-laser-engraver).

!!! "check that the laser head is level"
    This can be bjorked

#### Laser Prep

1. Print and assemble the alignment jig.
2. Mount to the laser base.
3. mount a viagrid blank into the jig.
4. Connect to computer, to lightburn
5. Open the viagrid template file.
6. click the layer showing the outline
   1. you can move it if you need to
7. activate it and trace
8. loosen the four screws and adjust until you get corners
9. tighten down.
10. lock the outline so it cant move. coupled with your machine now.

#### Running a job

1. drop in top copper
2. make sure that shit is the right size (put sizes here and how to adjust)
3. make inner bits layer 1, outer ring layer 30.
4. group it
5. snap it onto locked outline
6. cut that bad boi with settings

    - Speed: 100mm/s
    - Frequency: 35kHz
    - Q-Pulse Width: 1ns
    - Global Passes: 1
    - Mode: Fill
    - Line Interval (mm): 0.025
    - Scan Angle: 45deg
    - Number of Passes: 15
    - Angle Increment: 37deg
    - Fill all shapes at once: checked

7. stop after layer one, you aligned?
8. stop part way through and check, is your laser beefy and you're already done?
9. remove from jig
10. Sand down with 600 grit

### CNC Method
