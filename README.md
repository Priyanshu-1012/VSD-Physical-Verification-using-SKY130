# VSD-Physical-Verification-using-SKY130
![FINAL_VSDOpen 2022_PV1](https://user-images.githubusercontent.com/39450902/195810266-b72e2316-836d-4c07-8d91-7cc897d45852.jpg)

Repo for 5 day(10-14 Oct 2022) VSD-IAT Workshop: Physical Verification using SKY130.

## Day-1
### Installing Sky130 PDK to local machine

```
git clone https://github.com/RTimothyEdwards/open_pdks
cd open_pdks
configure --enable-sky130-pdk
make
sudo make install 
```
### Tools supported by open_pdks
* ***Magic***:      It does extraction, DRC, handles .def .gds .lef
* ***Klayout***:    Alternate layout editor and viewer(also do DRC)
* ***Openlane***:   Synthesis & PnR package based on Openroad tools
* ***Xschem***:     Schematic editing tool
* ***Netgen***:     LVS tool
* ***Ngspice***:    Analog simulation tool
* ***Xcircuit***:   alt. schematic capture tool
* ***IRsim***:      Switch level simulation and power analyzer
* ***qflow***:      alt. digital synthesis flow
* ***Iverilog***:   Verilog simulation and synthesis tool

### Links to tools
Tool | links
------------ | -------------
Magic | http://opencircuitdesign.com/magic
Klayout | https://www.klayout.de
Openlane | https://github.com/efabless/openlane
Xschem | https://github.com/StefanSchippers/xschem
Netgen | http://opencircuitdesign.com/netgen
iverilog | https://iverilog.icarus.com
qflow | http://opencircuitdesign.com/qflow
IRSIM | http://opencircuitdesign.com/irsim
Xcircuit | http://opencircuitdesign.com/xcircuit


## LAB for Day-1(INVERTER)

### Getting started...
* Check the installation by simply typing the name of the tool
* Making a directory *inverter*
* Creating folders *mag,xschem,ngspice*

#### Checking installations
<img width="960" alt="2022-10-13 (5)" src="https://user-images.githubusercontent.com/39450902/195818020-228a2581-8156-4010-ba76-a011fecdf3d4.png">

#### Making directories and files...Setting up
<img width="960" alt="2022-10-13 (7)" src="https://user-images.githubusercontent.com/39450902/195818003-79ede48b-d01f-4180-9bd6-a11e3c7be0f8.png">


#### Setup Commands

```ln -s /usr/share/pdk/sky130A/libs.tech/xschem/xschemrc```

```ln -s /usr/share/pdk/sky130A/libs.tech/ngspice/spinit .spiceinit```

```ln -s /usr/share/pdk/sky130A/libs.tech/magic/sky130A.magicrc .magicrc```

```ln -s /usr/share/pdk/sky130A/libs.tech/netgen/sky130A_setup.tcl setup.tcl```

### Xschem
<img width="960" alt="2022-10-13 (8)" src="https://user-images.githubusercontent.com/39450902/195817987-64426485-849d-404e-96e2-25abcc9f86ff.png">

#### Commands
```
cd ../xschem
xschem
```

### Magic
<img width="960" alt="2022-10-13 (10)" src="https://user-images.githubusercontent.com/39450902/195821934-d0344856-e68a-4dd8-9bbc-23a0827cdf42.png">
<img width="960" alt="2022-10-13 (18)" src="https://user-images.githubusercontent.com/39450902/195821959-b0a0c239-2d5a-4653-8403-3631385b7c79.png">
<img width="960" alt="2022-10-13 (17)" src="https://user-images.githubusercontent.com/39450902/195822024-3851e544-b1ec-489c-8cd0-cc86bf7917da.png">

#### Commands
```
cd ../mag
magic
```
## Making Inverter Schematic on Xschem

#### Making a New Schematic
<img width="960" alt="2022-10-13 (20)" src="https://user-images.githubusercontent.com/39450902/195823970-736e9157-0c13-4aa3-99ac-2b285a2978d4.png">

#### Press Insert key to open the insert symbol dialog box
<img width="960" alt="2022-10-13 (21)" src="https://user-images.githubusercontent.com/39450902/195823967-0eeb2b0c-efe9-4f8b-a172-974a3863b3e9.png">

#### Insert the pfet3 , nfet, ipin, iopins, opin and join them with wire(W key)

<img width="960" alt="2022-10-13 (33)" src="https://user-images.githubusercontent.com/39450902/195829396-c069b640-5cdf-4b08-b123-9bdd99593806.png">



<img width="960" alt="2022-10-13 (26)" src="https://user-images.githubusercontent.com/39450902/195823961-335de907-b283-4490-81ef-6c988091ec26.png">

#### Also change the W/L and number of fingers for the pfet and nfet by right clicking on the symbol

<img width="960" alt="2022-10-13 (37)" src="https://user-images.githubusercontent.com/39450902/195823951-4bebe4bc-fc0c-4bf7-aec2-b7c81704ceea.png">

##### Now go to symbol>make symbol from new schematic
##### then go to File>New Schematic
<img width="960" alt="2022-10-13 (38)" src="https://user-images.githubusercontent.com/39450902/195823950-34e7b1d3-563a-4231-a265-77eb2bf54d57.png">

#### Create New Schematic by adding inverter symbol, voltage sources, opins, GND and connect them with wires.
#### Add the voltage value for Vdd, input pulse, code for transient analysis and add the lib

<img width="960" alt="2022-10-13 (48)" src="https://user-images.githubusercontent.com/39450902/195823949-d7f8274f-fcb0-421c-a5fb-5c4ced7a3faa.png">

```".lib /usr/share/pdk/sky130A/libs.tech/ngspice/sky130.lib.spice tt"```

```".control tran 1n 1u plot V(in) V(out) .endc"```

#### Generate netlist, Save the Schematic as inverter_tb, and simulate! 
<img width="960" alt="2022-10-13 (49)" src="https://user-images.githubusercontent.com/39450902/195823945-6ad9454f-3673-45bd-91c4-7db918ec2474.png">

The result came out as expected! >> Now lets go to making the layout for inverter

## Importing Schematic to layout

```
cd ../mag
magic -d XR
```
then go File >> import SPICE >> inverter.spice

<img width="960" alt="2022-10-13 (55)" src="https://user-images.githubusercontent.com/39450902/195836652-5ae24e94-f7fa-4e91-bc7b-42f34f7c7846.png">
<img width="960" alt="2022-10-13 (56)" src="https://user-images.githubusercontent.com/39450902/195836687-342f2fce-fb77-442c-a2a7-f5e2286ab07a.png">

### Change the top, bottom guard rings; Source, drain coverage
 
For pfet select top guard ring via coverage and type 100. source via coverage =+40 drain via coverage = -40

and for nfet bottom guard ring via coverage = 100 source via covergae = +40 drain via coverage = -40

<img width="960" alt="2022-10-13 (65)" src="https://user-images.githubusercontent.com/39450902/195837280-25e4bcc9-0724-47e1-abfb-5fe3857d6289.png">
<img width="960" alt="2022-10-13 (63)" src="https://user-images.githubusercontent.com/39450902/195836735-4f22fb62-9271-4572-be8c-f983df9bf84f.png">

### Now complete the layout

![Screenshot (3)](https://user-images.githubusercontent.com/39450902/195836764-8a259cae-3f34-43e2-a475-634b4b61eb44.png)

#### Now click Save >> Autowrite
In Command window type following commands extraction, generate a spice netlist and then quit

```
extract do local
extract all
ext2spice lvs
ext2spice
quit
```


![Screenshot (4)](https://user-images.githubusercontent.com/39450902/195840608-2caeead7-6bdf-4a59-8ed7-0966fa7e564d.png)

### Now for LVS..

```
cd ../netgen
netgen -batch lvs "../mag/inverter.spice inverter" "../xschem/inverter.spice inverter"
```

![Screenshot (5)](https://user-images.githubusercontent.com/39450902/195841820-707249c5-f771-46b1-bf1f-9fad3804a0d1.png)

#### Due to some error my netlist didnt match...working on it(will update here once done)

![Screenshot (6)](https://user-images.githubusercontent.com/39450902/195842625-e5255084-1494-4c82-b90e-e66e90896c58.png)

<br>

## Day-2

### DRC & LVS

### Basics

* DRC : ensure the design meet all the fab rules for the mask
* LVS : ensure the layout matches the design schematic or any other similar form that define the design spec
* Data Formats : .cif, .GDSII(industry standard), OASIS
* Extraction : 2 step process(LAYOUT .mag file >> INTERMEDIATE .ext file >> NETLIST .spice file)
* Extraction options in magic
```
ext2spice lvs
ext2spice cthresh value
ext2spice scale on|off
ext2spice hierarchy on|off
ext2spice subcircuit top on|off
ext2spice global on|off
ext2spicemerge on|off
```
## LAB DAY-2

#### Create a proj directory

![Screenshot (7)](https://user-images.githubusercontent.com/39450902/195997118-61fcf710-7224-417f-98bd-eea22c10c587.png)

#### cif styles in magic

![Screenshot (8)](https://user-images.githubusercontent.com/39450902/195997120-d9cc27fd-7d21-4e28-b2ec-c2eafd7508af.png)

#### see the available top level cell useing ```cellname top```

![Screenshot (9)](https://user-images.githubusercontent.com/39450902/195997367-7769e6ea-8911-413e-94e9-9bf00f983104.png)

#### or by navigating Options >> Cell manager

![Screenshot (10)](https://user-images.githubusercontent.com/39450902/195997369-a8a595b9-acb9-402b-a2fb-a6e0165b39d7.png)

#### Then choose and2_1

![Screenshot (11)](https://user-images.githubusercontent.com/39450902/195997370-2ab31692-f04b-4044-93c6-19e355bfb57d.png)

#### we load the layout

![Screenshot (12)](https://user-images.githubusercontent.com/39450902/195997374-946fbaaf-d601-45fb-9eb7-64480c85d18c.png)

#### use ```cif istyle sky130(vendor)``` & then read gds file from lib (labels are blue coz they're being traeated as ports)

![Screenshot (13)](https://user-images.githubusercontent.com/39450902/195997377-6817c83e-2948-4c5a-830d-de1dba902860.png)


![Screenshot (15)](https://user-images.githubusercontent.com/39450902/195997385-a9f0f87a-df9e-4cff-8555-6418ebcf917c.png)

### Ports & Index

#### To enquire about ports use ```port index``` for more enquiry about say port with index 1... use ```port first``` then..
```
port 1 name
port 1 class
port 1 use
```
![Screenshot (18)](https://user-images.githubusercontent.com/39450902/195997392-e02e05da-9b9c-4624-a79f-d9e3a807c000.png)

#### and2_1 subckt definition
![Screenshot (19)](https://user-images.githubusercontent.com/39450902/195997395-efb3e12e-4548-4cf6-8bc9-f0fa1103ca11.png)
![Screenshot (20)](https://user-images.githubusercontent.com/39450902/195997397-d48f4a8b-d8fd-4df3-83c8-c68eaae98c19.png)

### Abstract views

#### read lef lib using ```lef read /usr/share/pdk/sky130A/libs.ref/sky130_fd_sc_hd/lef/sky130_fd_sc_hd.lef``` . Load and2_1 from cell manager, and the abstract view is shown...

![Screenshot (26)](https://user-images.githubusercontent.com/39450902/195997422-ab17d29b-36bf-467f-b6d6-23fee75b245e.png)

#### port order metadate isnt present

![Screenshot (27)](https://user-images.githubusercontent.com/39450902/195997424-952b44ed-e963-4df5-be92-f4b614ba2c2f.png)

#### use ```load test``` & instantiate the cell with command ```getcell sky130_fd_sc_hd__and2_1``` ....the abstract view is shown

![Screenshot (28)](https://user-images.githubusercontent.com/39450902/195997425-aee654d4-9827-4f03-af14-75c843102335.png)

#### we see layout....

![Screenshot (29)](https://user-images.githubusercontent.com/39450902/195997428-cb3dbd34-8689-4116-a08f-c09873c3999b.png)
![Screenshot (30)](https://user-images.githubusercontent.com/39450902/195997430-768cad53-6514-46d0-9964-eeb817ba6b67.png)
![Screenshot (31)](https://user-images.githubusercontent.com/39450902/195997432-9ebf939d-38da-4e1d-a68e-4a6ccae6f0d0.png)

#### start new session..

![Screenshot (32)](https://user-images.githubusercontent.com/39450902/195997433-6e4f4695-5dd6-4af3-b9d3-7e9ea003961f.png)

#### cell edited is from skywater pdks...check using ```path```

![Screenshot (33)](https://user-images.githubusercontent.com/39450902/195997435-19834f6d-1fba-4fc8-b6a7-260ad79415c1.png)

#### write into gds file

![Screenshot (34)](https://user-images.githubusercontent.com/39450902/195997438-b10d63ed-4fcc-4f77-a866-fcd86dbfd0d6.png)

#### LVS

```
  mkdir netgen 
  cd netgen
  cp /usr/share/pdk/sky130A/libs.tech/netgen/sky130A_setup.tcl ./setup.tcl
  cd ../mag
  magic -d XR sky130_fd_sc_hd__and2_1
  ext2spice lvs
  ext2spice lvs
  ext2spice
  quit
  cd ../netgen
  netgen -batch lvs "../mag/sky130_fd_sc_hd__and2_1.spice sky130_fd_sc_hd__and2_1" "/usr/share/pdk/sky130A/libs.ref/sky130_fd_sc_hd/spice/sky130_fd_sc_hd.spice sky130_fd_sc_hd__and2_1"
  ```
  #### Setup the XOR
  
  ```
    cd ../mag
  magic -d XR
  load sky130_fd_sc_hd__and2_1
  save altered
  load altered
  erase li
  flatten -nolabels xor_test
  load sky130_fd_sc_hd__and2_1
  xor -nolabels xor_test
  load xor_test
  quit
  magic -d XR
  load test3
  flatten -nolabels xor_test
  xor -nolabels xor_test
  load xor_test
  ```
  
  ![Screenshot (191)](https://user-images.githubusercontent.com/39450902/196000067-8ff3920e-a86e-48df-9e7c-ca5c35787885.png)
![Screenshot (192)](https://user-images.githubusercontent.com/39450902/196000070-b25bcf71-41a2-4ffb-b34c-f4ddcb474eaa.png)
![Screenshot (193)](https://user-images.githubusercontent.com/39450902/196000074-40160851-d005-4ca4-bef3-6bf5901a69c9.png)

<br></br>

## Day-3 (About DRC)

### Rules:

#### 1.Backend metal layer rules

* Width rule
* Spacing rule
* Wide spacing rule
* Notch rule
* Min & max area rules
* Min hole area rule
* Contact cut rules

#### 2.LI rules
#### 3.Frontend rules
#### 4.Wells, Taps and Net Rules
#### 5.Deeps N-Well and High Voltage Rules
#### 6.Device Rules(R,C,Diodes)
#### 7.Miscellaneous Rules and Latch-up, Antenna and Stress Rules
#### 8.Density rules
#### 9.Recomm manufac. and ERC rules

* Width rules
* Spacing (notch) rules
* Minimum area rules
* Overlap (surround) rules
* Extension rules
* Angle and off-grid rules
* Density rules (acceptable, rarely)

**ERC**
* ELectromigration
* Overvoltage conditions

## Lab DAY-3

#### Exercise-1

Getting started...
![Screenshot (35)](https://user-images.githubusercontent.com/39450902/196000889-4ac388ed-0ee2-40d2-825a-5346000b293c.png)
![Screenshot (36)](https://user-images.githubusercontent.com/39450902/196000893-9f5f42bc-ed90-44f2-8bd5-9b7f0e66a625.png)

Select and hit '?' on keyboard to get DRC report
![Screenshot (37)](https://user-images.githubusercontent.com/39450902/196000895-cf0b3160-0a5b-4906-bf96-24a3f9149c4e.png)
![Screenshot (38)](https://user-images.githubusercontent.com/39450902/196000897-e3a453ed-25d1-41c0-86e8-4c8e48f17367.png)

Press 'B' to check dimensions of the cursor box. Here the width was 0.06um  but the min width should be 0.14 microns.
To increase the width of the metal layer, we can either manually set the cursor box to the size required, then paint it using the middle mouse button/hover to the layer and hit 'P' on keyboard. Or we can do it with console commands by typing...

```box width 0.14um```

```paint m2```


![Screenshot (41)](https://user-images.githubusercontent.com/39450902/196000906-04a0090c-51f2-4f49-997d-34c5fc8a3289.png)
![Screenshot (42)](https://user-images.githubusercontent.com/39450902/196000907-53188426-d4e4-4a17-8077-ed21a29de86f.png)

Exercise 1b....DRC report

![Screenshot (43)](https://user-images.githubusercontent.com/39450902/196000910-4d2cbd8a-a142-477b-a782-8eb4c7f7dce6.png)

Its a spacing error...it can be resolved by moving either of the rectangles away.
Select a rectangles, and move it using 2-4-6-8 num keys (can also be done using the command ```move e 0.14um``` ...it moves the box 0.14um towards east>>)

![Screenshot (44)](https://user-images.githubusercontent.com/39450902/196000913-a7bf7b45-f7f5-466b-9607-3aafce9d19a5.png)

Exercise 1c...check the error

![Screenshot (45)](https://user-images.githubusercontent.com/39450902/196000916-0d0dab47-93b2-4e6c-964e-a40e2ca7c3e9.png)

Resolve this by increasing the seperation to by 0.4um either manually or by commands...your call

![Screenshot (47)](https://user-images.githubusercontent.com/39450902/196000921-bc0f38f5-9355-4ab7-b455-8e1052244db9.png)

Another width rule example(Notch rule)....resolve this my selecting half part('A') and stretching it(shift+num key)...increasing the width
Another way to do it is with ```stretch``` command..... ```stretch <direction> <measure>```


![Screenshot (49)](https://user-images.githubusercontent.com/39450902/196000926-f1c24627-039d-4a7c-97c4-8e3639f3dee9.png)


#### Exercise-2

2a. Via size error. Can be solved by simply stretching the via both horiz and vert.

![Screenshot (195)](https://user-images.githubusercontent.com/39450902/196018515-82d861d5-d417-4799-b117-54637b866e5f.png)
![Screenshot (53)](https://user-images.githubusercontent.com/39450902/196000934-227594a6-9898-4d21-924d-0fe94f82d677.png)

2b.  We got a large via with an array of contact cuts. To see the contact cuts >> run ```cif see xxx``` to check the cif layer names.
To see MCON(li for metal1), by using ```cif see MCON```

![Screenshot (54)](https://user-images.githubusercontent.com/39450902/196000935-d8444e33-7c02-4cf3-bf7e-d639339b97b1.png)

Use ```feedback why``` to get info about cif layer, and ```feedback clear``` to stop viewing the contact cuts.


2c. We got an overlap error. Fix by selecting the layer then use the ```box grow <direction> <measure>``` command as shown 
{'c' -> centre}.Then paint in a layer of metal1 to fix the overlap error.

![Screenshot (59)](https://user-images.githubusercontent.com/39450902/196000943-08b62a95-37ed-4cb1-80ea-a85ac5876ee2.png)

Now fix the size error by growing the box in e and w direction and paint it with m1

![Screenshot (60)](https://user-images.githubusercontent.com/39450902/196000947-385bcef8-a208-4481-baec-0802725cda6e.png)
![Screenshot (61)](https://user-images.githubusercontent.com/39450902/196000950-d8dcb47a-6c85-44ac-87e1-91153782aeb3.png)

2d. Generate via automatically >> use the wiring tool (spacebar). By SHIFT+ left click >> we can move up a metal layer till metal5. Similarly, we can move down layers with the SHIFT+right click until the metal interconnect. To see vias use...

```
Cif see MCON
Cif see VIA1
Cif see VIA2
Cif see VIA3
Cif see VIA4
```
![Screenshot (62)](https://user-images.githubusercontent.com/39450902/196000952-ec3eaab5-69b0-4a54-85fa-4141f8247eea.png)

#### Exercise-3

3a.Min area rule... simply stretch to fix it

![Screenshot (63)](https://user-images.githubusercontent.com/39450902/196000953-e19558a8-02b8-42f3-9a7f-c0f26456bc40.png)
![Screenshot (64)](https://user-images.githubusercontent.com/39450902/196000957-e1b7ec14-c855-4c11-ba7c-8e3c540fc679.png)
![Screenshot (65)](https://user-images.githubusercontent.com/39450902/196000959-2e4b808a-22cb-4fd8-a045-fc80cc6f2d01.png)


3b. Min. hole area rule...To see this error >> run Magic in the full DRC mode(menu button DRC >> DRC complete). Then run a DRC report.

![Screenshot (67)](https://user-images.githubusercontent.com/39450902/196000963-d9c8086d-930f-4dfc-97c0-1b0f602b1106.png)

Fix this by manually erasing sections of metal till the hole is big enough to pass DRC.

![Screenshot (68)](https://user-images.githubusercontent.com/39450902/196000966-b1810866-a413-4542-8b00-7bf18b6815fc.png)


#### Exercise-4

4a. Its a well error(the wells don't have taps). N-well shows an error  coz its floating(the P-well doesn't since p-wells aren't actually considered... unless they're in deep n-wells(instead treated as psub).

![Screenshot (69)](https://user-images.githubusercontent.com/39450902/196000967-a5802ecf-e49a-4d0b-8571-95d4c22e48b3.png)

fix this by adding n-type material(nsubstratendiff) into the n-well. Then connect a layer of local interconnect to tap(nsubstratencontact). 

![Screenshot (70)](https://user-images.githubusercontent.com/39450902/196000971-59f49569-acd9-4fea-9fa5-047550d68b51.png)

Leads to new errors..solve these overlap and surround errors by stretching, adding li.

![Screenshot (71)](https://user-images.githubusercontent.com/39450902/196000972-428ca802-8a55-4958-9fec-793174be0d87.png)


4b. *The p well has to be connected to a contact if it has a tap*. Add psubstratepcontact, some li, and adjust the areas of the layers, we get a DRC correct layout.

![Screenshot (196)](https://user-images.githubusercontent.com/39450902/196019876-79bdfc5e-39d5-4ca4-94db-344d12d102d0.png)
![Screenshot (72)](https://user-images.githubusercontent.com/39450902/196000974-887b82af-280d-4dcc-902b-51ce7a961980.png)

4c. Error in deep n-well 

![Screenshot (73)](https://user-images.githubusercontent.com/39450902/196000978-bc97e6ba-0c5a-4455-bdca-f114f21b07b1.png)

Grow the deep n-well >> move it away from the n-well(4b) {its interacting with it}. Add an n-well overlap around the deep n-well(wire tool) >> add in a tap layer with an interconnect. 

![Screenshot (75)](https://user-images.githubusercontent.com/39450902/196000985-894c6544-eb4d-4d88-a12d-7cf55e067581.png)
![Screenshot (76)](https://user-images.githubusercontent.com/39450902/196020249-fbe4acc9-4757-49e8-8f6e-b2c56261ef5e.png)

Also for deep n-wells >> add a full setup with guard rings (Devices 1 >> deep n-well region)

![Screenshot (76)](https://user-images.githubusercontent.com/39450902/196000987-1d1a588f-d122-403c-bfba-0986f9ac95a3.png)


#### Exercise-5

![Screenshot (77)](https://user-images.githubusercontent.com/39450902/196000989-e246ea3d-2b83-4937-a4fc-a6be26024c36.png)
![Screenshot (78)](https://user-images.githubusercontent.com/39450902/196000991-d6c836c4-bd87-4209-81bd-484bfa1aec1f.png)
![Screenshot (79)](https://user-images.githubusercontent.com/39450902/196001002-c1f2d15f-bb7a-462b-9204-6a170b30184f.png)
![Screenshot (80)](https://user-images.githubusercontent.com/39450902/196001004-6f2be68a-831e-4033-bf57-10d7bd3e0fb0.png)
![Screenshot (81)](https://user-images.githubusercontent.com/39450902/196001007-4e46396f-d3a6-4649-8514-8806721a22ce.png)
![Screenshot (82)](https://user-images.githubusercontent.com/39450902/196001011-f0324c1a-9f97-4e77-8204-8bb559c122ef.png)
![Screenshot (83)](https://user-images.githubusercontent.com/39450902/196001014-5054b0e7-b579-4643-b38b-8f9447574b8a.png)
![Screenshot (84)](https://user-images.githubusercontent.com/39450902/196001018-891eeb1a-3f5f-4f79-ab7c-2b509b33b627.png)
![Screenshot (85)](https://user-images.githubusercontent.com/39450902/196001021-93398400-1313-40be-8b2a-ee1cc8c9e2ab.png)
![Screenshot (86)](https://user-images.githubusercontent.com/39450902/196001024-03039072-af5b-4d58-b772-1870c6c15489.png)
![Screenshot (87)](https://user-images.githubusercontent.com/39450902/196001025-34d44b2b-4789-4fa3-a6dc-015e08ef0570.png)
![Screenshot (88)](https://user-images.githubusercontent.com/39450902/196001028-f94e0049-455c-46b4-8698-32a4a006f07e.png)
![Screenshot (89)](https://user-images.githubusercontent.com/39450902/196001029-245d46b3-8538-4e8a-a523-76d8fe1311b6.png)
![Screenshot (90)](https://user-images.githubusercontent.com/39450902/196001031-6b7d2e0c-625f-4294-928a-539e1d90dcd3.png)
![Screenshot (91)](https://user-images.githubusercontent.com/39450902/196001034-2fa5082b-8e17-4922-a018-f3d15e51299a.png)
![Screenshot (92)](https://user-images.githubusercontent.com/39450902/196001036-1f5a1f0a-af71-4ea9-8076-1ec1dba19155.png)
![Screenshot (93)](https://user-images.githubusercontent.com/39450902/196001038-8e84b77c-24a8-45e6-976e-46258ee5d7c3.png)
![Screenshot (94)](https://user-images.githubusercontent.com/39450902/196001045-bc1d9592-18e3-4040-8353-e49a4e322877.png)
![Screenshot (95)](https://user-images.githubusercontent.com/39450902/196001050-3920986e-9ec4-49f2-828e-77e19a1753ca.png)
![Screenshot (97)](https://user-images.githubusercontent.com/39450902/196001054-432fba30-2d22-46ba-936c-9de4473d2e31.png)
![Screenshot (98)](https://user-images.githubusercontent.com/39450902/196001059-bf93ce9e-bf90-45f8-922a-adabb9634fef.png)
![Screenshot (99)](https://user-images.githubusercontent.com/39450902/196001060-73714a04-a298-4136-a23d-6ff8dc14137c.png)
![Screenshot (101)](https://user-images.githubusercontent.com/39450902/196001061-47683d89-e0b1-4702-8b3d-60ed3ac8c322.png)
![Screenshot (100)](https://user-images.githubusercontent.com/39450902/196001063-a3752e5c-ad4a-4fd6-928a-950c7e526e7d.png)
![Screenshot (102)](https://user-images.githubusercontent.com/39450902/196001067-75dc812b-fd76-4b00-afd5-d33e56a27fbb.png)
![Screenshot (103)](https://user-images.githubusercontent.com/39450902/196001070-1fc28303-2784-4197-8831-315465df2d3a.png)
![Screenshot (104)](https://user-images.githubusercontent.com/39450902/196001075-404e1052-90c6-440c-85e0-b6bfc2d7a86b.png)
![Screenshot (105)](https://user-images.githubusercontent.com/39450902/196001077-6b894740-3032-433d-847f-13b1408930cb.png)
![Screenshot (106)](https://user-images.githubusercontent.com/39450902/196001080-14ad160a-c3cd-4a4a-95c5-f391b488a21b.png)
![Screenshot (107)](https://user-images.githubusercontent.com/39450902/196001081-ec08cbfe-ca86-4985-91e8-cbeb2a3e85b1.png)
![Screenshot (108)](https://user-images.githubusercontent.com/39450902/196001085-940ea6df-74f0-455a-825f-5ac2369a8c2d.png)
![Screenshot (109)](https://user-images.githubusercontent.com/39450902/196001087-280f641c-036b-4429-9572-f76c0b7d5688.png)
![Screenshot (110)](https://user-images.githubusercontent.com/39450902/196001088-1a290af9-4912-43d8-a2b7-6f95ba9655f7.png)
![Screenshot (111)](https://user-images.githubusercontent.com/39450902/196001091-7bcc7e3b-9e64-4552-9cb1-fd9dbd1e712b.png)
![Screenshot (112)](https://user-images.githubusercontent.com/39450902/196001093-28cb7ecf-3e28-4037-9c89-b19e23102139.png)
![Screenshot (113)](https://user-images.githubusercontent.com/39450902/196001095-f4086a0f-1cee-4afb-acb0-65cdf1728b3c.png)
![Screenshot (114)](https://user-images.githubusercontent.com/39450902/196001098-d5e0821f-624c-46fb-85c9-92b2bb71289f.png)
![Screenshot (115)](https://user-images.githubusercontent.com/39450902/196001101-f0ce763b-491e-4d58-af02-75bbc253596a.png)
![Screenshot (116)](https://user-images.githubusercontent.com/39450902/196001105-cbf6c84e-63ae-47ec-a98c-a1e0aecbc5a9.png)






### LAB DAY-5
![Screenshot (117)](https://user-images.githubusercontent.com/39450902/196001174-9ba833d4-b057-484c-bb04-3288628e25e9.png)
![Screenshot (118)](https://user-images.githubusercontent.com/39450902/196001175-d4a8467b-1c28-4a9f-8354-5a580918b162.png)
![Screenshot (119)](https://user-images.githubusercontent.com/39450902/196001177-35624621-df53-463a-9ddc-aeef7d5125ad.png)
![Screenshot (120)](https://user-images.githubusercontent.com/39450902/196001181-410bbae3-36e5-415d-a6c3-1d5effa2cbec.png)
![Screenshot (121)](https://user-images.githubusercontent.com/39450902/196001182-74673e4f-6be9-4fa1-9f03-f3821b39472e.png)
![Screenshot (122)](https://user-images.githubusercontent.com/39450902/196001185-bb3121c3-9fca-415a-9be8-d7e5ea2bb442.png)
![Screenshot (123)](https://user-images.githubusercontent.com/39450902/196001187-afe5fa7b-a8de-42f1-b9be-591747d3e1e9.png)
![Screenshot (124)](https://user-images.githubusercontent.com/39450902/196001189-5b0db68f-66ed-4f97-86dc-993d3c5a8046.png)
![Screenshot (125)](https://user-images.githubusercontent.com/39450902/196001191-9b502023-9204-4146-9558-f5037867630f.png)
![Screenshot (126)](https://user-images.githubusercontent.com/39450902/196001198-0a00a62a-73bf-41f4-af0c-dc1a05fc322f.png)
![Screenshot (127)](https://user-images.githubusercontent.com/39450902/196001205-b0e4ccf5-556c-407f-a6e7-a81142513e89.png)
![Screenshot (128)](https://user-images.githubusercontent.com/39450902/196001206-c614cd95-7567-477d-bc87-3775a376c584.png)
![Screenshot (129)](https://user-images.githubusercontent.com/39450902/196001207-fc293192-2546-4abd-a3e7-976fb5a4b8e2.png)
![Screenshot (130)](https://user-images.githubusercontent.com/39450902/196001209-40250937-d326-4926-8169-260182db75d4.png)
![Screenshot (131)](https://user-images.githubusercontent.com/39450902/196001212-2482cfd7-7ec3-4f1e-96d6-0e6119668c2a.png)
![Screenshot (132)](https://user-images.githubusercontent.com/39450902/196001213-6b5be830-0daf-4ba5-85cc-39fbc11ebb2c.png)
![Screenshot (133)](https://user-images.githubusercontent.com/39450902/196001214-a71dfb2c-7497-404e-9db4-294f642e03ba.png)
![Screenshot (134)](https://user-images.githubusercontent.com/39450902/196001215-91f72a1d-4675-430f-a884-a9a4c781ca43.png)
![Screenshot (135)](https://user-images.githubusercontent.com/39450902/196001217-28d0c370-3fec-4a2c-a522-b743efafab7b.png)
![Screenshot (136)](https://user-images.githubusercontent.com/39450902/196001218-f7619f46-49b7-49dc-9ba3-3541654b4b86.png)
![Screenshot (137)](https://user-images.githubusercontent.com/39450902/196171408-c2f1b453-5f95-4d36-ac92-e0848930d56c.png)
![Screenshot (138)](https://user-images.githubusercontent.com/39450902/196171484-363afab0-26da-4ce4-b48a-085fc86123b7.png)
![Screenshot (139)](https://user-images.githubusercontent.com/39450902/196171493-a6630556-2e7b-42a5-ad91-96df2174d146.png)
![Screenshot (140)](https://user-images.githubusercontent.com/39450902/196171501-1b1d10c8-2bb4-48ed-9e8b-e0b23627189c.png)
![Screenshot (141)](https://user-images.githubusercontent.com/39450902/196171507-6d427f40-4810-453e-8abd-75654b320986.png)
![Screenshot (142)](https://user-images.githubusercontent.com/39450902/196171523-9f3aebd0-2abd-4ff3-907b-bcd5841fe5a9.png)
![Screenshot (143)](https://user-images.githubusercontent.com/39450902/196171530-0af65f78-1f01-449a-9e48-e2e093b84a8f.png)
![Screenshot (144)](https://user-images.githubusercontent.com/39450902/196171540-dd54846f-1b7e-46f5-9c2a-9b6e1a2a9c37.png)
![Screenshot (145)](https://user-images.githubusercontent.com/39450902/196171544-30b668cb-a4e5-498b-88bb-84e9e29c6b38.png)
![Screenshot (147)](https://user-images.githubusercontent.com/39450902/196171569-e7489869-5fe0-4c5c-a77b-d87db04f7a42.png)
![Screenshot (148)](https://user-images.githubusercontent.com/39450902/196171577-c6c8f4c4-6953-4933-8da8-6edbddaeb091.png)
![Screenshot (149)](https://user-images.githubusercontent.com/39450902/196171587-f4a94d2d-10e1-49b5-bf34-2c07fb18ccb0.png)
![Screenshot (150)](https://user-images.githubusercontent.com/39450902/196171606-dee97a9d-dfd8-4da3-af7a-4adc8cf63df5.png)
![Screenshot (151)](https://user-images.githubusercontent.com/39450902/196171613-bdc4ec2d-18dd-412e-97b0-8d6c0521b804.png)
![Screenshot (152)](https://user-images.githubusercontent.com/39450902/196171616-9d0c1db2-094a-4be7-8bcb-c67eb04ac477.png)
![Screenshot (153)](https://user-images.githubusercontent.com/39450902/196171618-38e132ed-d574-4ae6-8518-942c620d2051.png)
![Screenshot (154)](https://user-images.githubusercontent.com/39450902/196171660-1ae27d45-0dd9-4fbe-81fa-fb59bd0759e8.png)
![Screenshot (155)](https://user-images.githubusercontent.com/39450902/196171666-7caade85-ef5c-43cb-b8e9-917718e8c8b8.png)
![Screenshot (156)](https://user-images.githubusercontent.com/39450902/196171673-6c1b423f-b550-4371-b17f-c13546df53d8.png)
![Screenshot (157)](https://user-images.githubusercontent.com/39450902/196171675-8e7799bc-4180-4205-8b1c-2d36c67496bb.png)
![Screenshot (158)](https://user-images.githubusercontent.com/39450902/196171684-5f4170e4-7881-4092-9f0b-6aa60244d44c.png)
![Screenshot (159)](https://user-images.githubusercontent.com/39450902/196171689-b7b08b53-0746-44c4-934a-e612656af34c.png)
![Screenshot (160)](https://user-images.githubusercontent.com/39450902/196171693-28abb7e6-0060-49b8-92e5-c012eac299dd.png)
![Screenshot (161)](https://user-images.githubusercontent.com/39450902/196171697-6696d7cc-0bcf-4a73-8471-1999155fb907.png)
![Screenshot (162)](https://user-images.githubusercontent.com/39450902/196171703-95e07eef-37a3-4875-9492-8f2aa45d924a.png)
![Screenshot (163)](https://user-images.githubusercontent.com/39450902/196171705-b0ed4126-2f68-4f58-b90d-0fbf34aa849d.png)
![Screenshot (164)](https://user-images.githubusercontent.com/39450902/196171711-b97c9e39-232b-4c49-b872-701f2ee3a405.png)
![Screenshot (165)](https://user-images.githubusercontent.com/39450902/196171719-28adbce4-4284-48db-9370-3fd9f930a698.png)
![Screenshot (166)](https://user-images.githubusercontent.com/39450902/196171732-e27b59ad-de62-4076-9183-1a2d8f8d5ae8.png)
![Screenshot (167)](https://user-images.githubusercontent.com/39450902/196171739-7790f112-b4a7-4cdd-a242-1f7f68c8daf7.png)
![Screenshot (168)](https://user-images.githubusercontent.com/39450902/196171744-c03e1763-65d1-45fd-a78f-b920076916a1.png)
![Screenshot (169)](https://user-images.githubusercontent.com/39450902/196171750-4ea42e1d-ebf9-4fe2-9584-837f02cfe6f6.png)
![Screenshot (170)](https://user-images.githubusercontent.com/39450902/196171763-96c8f79b-f101-4da0-9c35-f2c5815f88bc.png)
![Screenshot (171)](https://user-images.githubusercontent.com/39450902/196171769-9147bac5-4fd4-485b-bc2c-4193a23ccd2d.png)
![Screenshot (172)](https://user-images.githubusercontent.com/39450902/196171777-42a75d57-3ef6-41de-84f9-f5b2210e8f07.png)
![Screenshot (173)](https://user-images.githubusercontent.com/39450902/196171778-e6a77cbd-4fc6-47c3-bdc9-6ce61c44d869.png)
![Screenshot (174)](https://user-images.githubusercontent.com/39450902/196171782-16088a74-ded1-42a8-b263-e2e2f6fa92af.png)
![Screenshot (175)](https://user-images.githubusercontent.com/39450902/196171785-399fa962-d5f2-4cb9-b71b-13a09c791b41.png)
![Screenshot (176)](https://user-images.githubusercontent.com/39450902/196171790-fdebe7c4-c30d-44b4-8333-9acbc6070d89.png)
![Screenshot (177)](https://user-images.githubusercontent.com/39450902/196171804-797d8111-7194-4545-9ede-29e7eb685fb5.png)
![Screenshot (178)](https://user-images.githubusercontent.com/39450902/196171809-ce570e13-6224-4745-b0ef-b08218cf9640.png)
![Screenshot (179)](https://user-images.githubusercontent.com/39450902/196171814-2db9bb9f-6bdb-4e24-8aef-3078b1b24ed0.png)
![Screenshot (180)](https://user-images.githubusercontent.com/39450902/196171820-03e422c9-fce1-46a2-8e77-caf26ce5de24.png)
![Screenshot (181)](https://user-images.githubusercontent.com/39450902/196171824-fe1f2eba-6fa1-4fdc-96c1-e5733629c9c3.png)
![Screenshot (182)](https://user-images.githubusercontent.com/39450902/196171827-d7bf0635-a381-4ce1-b8bf-10f118bdb135.png)
![Screenshot (183)](https://user-images.githubusercontent.com/39450902/196171833-cab90bfa-5886-49a2-acd5-3b7dff44f0cd.png)
![Screenshot (184)](https://user-images.githubusercontent.com/39450902/196171852-d8e05b27-eb40-4c08-92c9-b646710469d7.png)
![Screenshot (185)](https://user-images.githubusercontent.com/39450902/196171856-2cea24ec-87bb-45a6-a494-cf9ea11cbb7f.png)
![Screenshot (186)](https://user-images.githubusercontent.com/39450902/196171863-fc8d0d63-0014-4183-97f1-e08dbe7cb5c3.png)
![Screenshot (187)](https://user-images.githubusercontent.com/39450902/196171869-d6f28653-1302-4c89-8ef9-6868f265e71e.png)
![Screenshot (188)](https://user-images.githubusercontent.com/39450902/196171877-e18fd57b-e5aa-414a-bd2a-4934756d33cc.png)
![Screenshot (189)](https://user-images.githubusercontent.com/39450902/196171880-9a60e5d0-cc9c-4868-bded-70cc489cc19e.png)
![Screenshot (180)](https://user-images.githubusercontent.com/39450902/196171961-ffbc9b0d-b567-4d82-973c-b7fa82ec406d.png)
![Screenshot (181)](https://user-images.githubusercontent.com/39450902/196171965-73e4353c-5a92-4ab1-963d-ca5ae9147b30.png)
![Screenshot (182)](https://user-images.githubusercontent.com/39450902/196171968-cf8191e8-e356-4b13-9dc7-d8db553b7aa1.png)
![Screenshot (183)](https://user-images.githubusercontent.com/39450902/196171972-67d64af7-aaf4-4bfe-b8db-a9afa26e3dc7.png)
![Screenshot (184)](https://user-images.githubusercontent.com/39450902/196171985-e98859b6-d61e-4fca-9660-aa33c2084eac.png)
![Screenshot (185)](https://user-images.githubusercontent.com/39450902/196171987-cb36128b-baf7-4cfa-aba8-82325ec912e5.png)
![Screenshot (186)](https://user-images.githubusercontent.com/39450902/196171989-9c192aaf-293a-4b2c-b192-4109293c231e.png)
![Screenshot (187)](https://user-images.githubusercontent.com/39450902/196171992-ccace8e7-9b8b-443d-9bb2-5f7e6a290457.png)
![Screenshot (188)](https://user-images.githubusercontent.com/39450902/196172005-b69eda04-6b83-4496-b7c6-50e25c140355.png)
![Screenshot (189)](https://user-images.![Screenshot (190)](https://user-images.githubusercontent.com/39450902/196172038-53547c5b-9e2c-4aaa-a2b4-99c28cd87cbf.png)
githubusercontent.com/39450902/196172009-012b44a0-cc21-47f0-8f13-41431394a662.png)
