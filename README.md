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

#### we see layout...

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

![Screenshot (35)](https://user-images.githubusercontent.com/39450902/196000889-4ac388ed-0ee2-40d2-825a-5346000b293c.png)
![Screenshot (36)](https://user-images.githubusercontent.com/39450902/196000893-9f5f42bc-ed90-44f2-8bd5-9b7f0e66a625.png)
![Screenshot (37)](https://user-images.githubusercontent.com/39450902/196000895-cf0b3160-0a5b-4906-bf96-24a3f9149c4e.png)
![Screenshot (38)](https://user-images.githubusercontent.com/39450902/196000897-e3a453ed-25d1-41c0-86e8-4c8e48f17367.png)
![Screenshot (39)](https://user-images.githubusercontent.com/39450902/196000900-930ca23f-9752-4bc7-9179-debb287aabe1.png)
![Screenshot (40)](https://user-images.githubusercontent.com/39450902/196000905-71248683-17d5-4161-b399-0af8ef66e6e0.png)
![Screenshot (41)](https://user-images.githubusercontent.com/39450902/196000906-04a0090c-51f2-4f49-997d-34c5fc8a3289.png)
![Screenshot (42)](https://user-images.githubusercontent.com/39450902/196000907-53188426-d4e4-4a17-8077-ed21a29de86f.png)
![Screenshot (43)](https://user-images.githubusercontent.com/39450902/196000910-4d2cbd8a-a142-477b-a782-8eb4c7f7dce6.png)
![Screenshot (44)](https://user-images.githubusercontent.com/39450902/196000913-a7bf7b45-f7f5-466b-9607-3aafce9d19a5.png)
![Screenshot (45)](https://user-images.githubusercontent.com/39450902/196000916-0d0dab47-93b2-4e6c-964e-a40e2ca7c3e9.png)
![Screenshot (46)](https://user-images.githubusercontent.com/39450902/196000917-e832f994-ec70-4ff0-91fd-f8a42b6acbe9.png)
![Screenshot (47)](https://user-images.githubusercontent.com/39450902/196000921-bc0f38f5-9355-4ab7-b455-8e1052244db9.png)
![Screenshot (48)](https://user-images.githubusercontent.com/39450902/196000925-900733ee-9f96-44fd-88e3-2082ee50070a.png)
![Screenshot (49)](https://user-images.githubusercontent.com/39450902/196000926-f1c24627-039d-4a7c-97c4-8e3639f3dee9.png)
![Screenshot (51)](https://user-images.githubusercontent.com/39450902/196000929-ece0a861-5b2f-4935-ac94-bcbd67208ec5.png)
![Screenshot (52)](https://user-images.githubusercontent.com/39450902/196000932-daa02594-6bdf-4610-8445-b6a8fdc93575.png)

#### Exercise-2

![Screenshot (53)](https://user-images.githubusercontent.com/39450902/196000934-227594a6-9898-4d21-924d-0fe94f82d677.png)
![Screenshot (54)](https://user-images.githubusercontent.com/39450902/196000935-d8444e33-7c02-4cf3-bf7e-d639339b97b1.png)
![Screenshot (59)](https://user-images.githubusercontent.com/39450902/196000943-08b62a95-37ed-4cb1-80ea-a85ac5876ee2.png)
![Screenshot (60)](https://user-images.githubusercontent.com/39450902/196000947-385bcef8-a208-4481-baec-0802725cda6e.png)
![Screenshot (61)](https://user-images.githubusercontent.com/39450902/196000950-d8dcb47a-6c85-44ac-87e1-91153782aeb3.png)
![Screenshot (62)](https://user-images.githubusercontent.com/39450902/196000952-ec3eaab5-69b0-4a54-85fa-4141f8247eea.png)
![Screenshot (63)](https://user-images.githubusercontent.com/39450902/196000953-e19558a8-02b8-42f3-9a7f-c0f26456bc40.png)
![Screenshot (64)](https://user-images.githubusercontent.com/39450902/196000957-e1b7ec14-c855-4c11-ba7c-8e3c540fc679.png)
![Screenshot (65)](https://user-images.githubusercontent.com/39450902/196000959-2e4b808a-22cb-4fd8-a045-fc80cc6f2d01.png)
![Screenshot (66)](https://user-images.githubusercontent.com/39450902/196000960-5d6a1cba-9e21-4d73-8a1c-6d60c30e4c7c.png)
![Screenshot (67)](https://user-images.githubusercontent.com/39450902/196000963-d9c8086d-930f-4dfc-97c0-1b0f602b1106.png)
![Screenshot (68)](https://user-images.githubusercontent.com/39450902/196000966-b1810866-a413-4542-8b00-7bf18b6815fc.png)
![Screenshot (69)](https://user-images.githubusercontent.com/39450902/196000967-a5802ecf-e49a-4d0b-8571-95d4c22e48b3.png)
![Screenshot (70)](https://user-images.githubusercontent.com/39450902/196000971-59f49569-acd9-4fea-9fa5-047550d68b51.png)
![Screenshot (71)](https://user-images.githubusercontent.com/39450902/196000972-428ca802-8a55-4958-9fec-793174be0d87.png)
![Screenshot (72)](https://user-images.githubusercontent.com/39450902/196000974-887b82af-280d-4dcc-902b-51ce7a961980.png)
![Screenshot (73)](https://user-images.githubusercontent.com/39450902/196000978-bc97e6ba-0c5a-4455-bdca-f114f21b07b1.png)
![Screenshot (74)](https://user-images.githubusercontent.com/39450902/196000981-cc883228-f01b-49e5-9729-08d23d3ba1a8.png)
![Screenshot (75)](https://user-images.githubusercontent.com/39450902/196000985-894c6544-eb4d-4d88-a12d-7cf55e067581.png)
![Screenshot (76)](https://user-images.githubusercontent.com/39450902/196000987-1d1a588f-d122-403c-bfba-0986f9ac95a3.png)
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
