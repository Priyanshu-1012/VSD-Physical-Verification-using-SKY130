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


<img width="960" alt="2022-10-13 (20)" src="https://user-images.githubusercontent.com/39450902/195823970-736e9157-0c13-4aa3-99ac-2b285a2978d4.png">
<img width="960" alt="2022-10-13 (21)" src="https://user-images.githubusercontent.com/39450902/195823967-0eeb2b0c-efe9-4f8b-a172-974a3863b3e9.png">
<img width="960" alt="2022-10-13 (22)" src="https://user-images.githubusercontent.com/39450902/195823963-fc015fe3-fa6c-44e7-815f-a46bc11f586d.png">
<img width="960" alt="2022-10-13 (38)" src="https://user-images.githubusercontent.com/39450902/195823950-34e7b1d3-563a-4231-a265-77eb2bf54d57.png">
<img width="960" alt="2022-10-13 (26)" src="https://user-images.githubusercontent.com/39450902/195823961-335de907-b283-4490-81ef-6c988091ec26.png">
<img width="960" alt="2022-10-13 (37)" src="https://user-images.githubusercontent.com/39450902/195823951-4bebe4bc-fc0c-4bf7-aec2-b7c81704ceea.png">
<img width="960" alt="2022-10-13 (49)" src="https://user-images.githubusercontent.com/39450902/195823945-6ad9454f-3673-45bd-91c4-7db918ec2474.png">
<img width="960" alt="2022-10-13 (48)" src="https://user-images.githubusercontent.com/39450902/195823949-d7f8274f-fcb0-421c-a5fb-5c4ced7a3faa.png">

















