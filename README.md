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
