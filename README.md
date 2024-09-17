# vsd_openlane_Soc-Design_workshop
This repository cover RTL to GDS|| chip design steps which are done through openLANE flow .It cover all contents of workshop organised by VSD System Design in colloboration with NASSCOM.

# Day1 - Inception of  open-source EDA,OpenLANE and sky130 PDK
**Introduction to OpenLANE**

OpenlANE is opensource Flow which contain different tools Which are require in different steps of chip design. Yosys tools is use for RTL synthesis.Magic tool is use for floorplanning and layout.OpenSTA is use for STA.

**Different steps of chip design done through openlane**

 RTL synthesis- In this step Design is modelled through hardware descripting language like verilog.Yosys tool is use here for RTL synthesis.

 logic synthesis- converting the RTL functionality into hardware is referred as logic synthesis.

 Floorplanning- The arrangement of preplaced IPs, cells, flipflop on chips is called floorplanning.Actually size of core and die is decide in floorplanning step.

 Placement- AFter floorplanning,there is placement in which cells,flipflops,gates are arranged and placed in such way that they should be at proper distance from input and output pins so that less wire require for connection.

 CLock tree Synthesis- Clock should be placed such that all flip flops connected to respective clock should get pulse at same time so that skew should be minimum.So basically tree shape or H shape is made.

 Routing- In this step,connectionof cells are done.

 STA(Static time analysis)- timing verification,timing analysis is done in this step ,OpenSTA is use here.
 

### Path require for openlane design steps 

```bash
cd Desktop/work/tools/openlane_working_dir/openlane

Start docker in openlane just type 'docker'
```
After opening docker enter in interactive mode by following command
```bash
./flow.tcl -interactive
```
![VirtualBox_soc workshop_16_09_2024_09_48_42 openlane design](https://github.com/user-attachments/assets/5c9fa208-24f8-4c8e-9e6a-0ceaf88bd553)

###Importing Package and Preparing design in picorv32a

following commands is use

```bash
package require openlane 0.9

prep -design picorv32a
```
![VirtualBox_soc workshop_16_09_2024_09_49_07 preparing design in picorv 32a](https://github.com/user-attachments/assets/7b5cc008-65fc-4c50-b96e-18a3e24b1512)

### Synthesis
For running synthesis command is 

```bash
run_synthesis
```
![VirtualBox_soc workshop_11_09_2024_20_02_06 synthesis](https://github.com/user-attachments/assets/bac2b7bc-ebdf-44a7-a7d3-92a1fee7b2da)

### To see the results of synthesis
```bash
cd Desktop/work/tools/openlane/designs/picorv32a/runs/latest date folder/results/synthesis/less picorv32a.synthesis.v
```

designs directory
![VirtualBox_soc workshop_11_09_2024_20_05_08 design](https://github.com/user-attachments/assets/215797ca-920c-4e37-86cd-ccb66c7acd30)


picorv32a directory
![VirtualBox_soc workshop_11_09_2024_20_06_01 picorv32a](https://github.com/user-attachments/assets/d3ae6429-1c22-46a8-81e2-fdb83733720f)

runs command and going to latest folder
![VirtualBox_soc workshop_11_09_2024_20_07_51 latest folder](https://github.com/user-attachments/assets/c02dc21a-efd7-4d87-baf0-811d2ea5188f)

**Results of Synthesis**

![VirtualBox_soc workshop_11_09_2024_20_20_39 result of synthesis](https://github.com/user-attachments/assets/1e10d5aa-65c4-4b16-8cb8-9714e771b427)

```bash
Flip flop ratio
Number of cells=14876
Number of D flip flop=1613
Ratio=number of flip flop/number of cells
1613/14876=0.1084

So D flipflop % =0.1084*100
                =10.84%
```

# Day2 - Good Floorplan vs bad floorplan and introduction to library cells
**some terms to be discussed**

Netlist- It shows the connection of different components in logic synthesis

Core-It is a section of chip where fundamnetal logic of the design is placed

Die- It consist of core, is small semiconductor material specimen on which fundamental circuit is fabricated 

Utilization Factor- It is the ratio of area occupied by netlist to the total area of core

Aspect ratio- Height of core /width of core

Pre placed cells- There are some IPs and blocks having user defined location and are placed in chip before automated placement and routing ,are calleed pre placed cells.

Decoupling capacitor- In electronics, a decoupling capacitor is a capacitor used to decouple (i.e-prevent electrical energy from transfering to one part of circuit from other part)

 ###FLoorplan
 
###Inside README.md File
for going in README.md following is the commands
```bash
cd Desktop/work/tools/openlane_working_dir/openlane/Configuration/less README.md
```
 ![VirtualBox_soc workshop_11_09_2024_20_25_08 readme](https://github.com/user-attachments/assets/c51af1f3-bb61-42d8-8baa-101de9c956e5)

 in README file different variables are there

 ```bash
less floorplan.tcl
```
here we get default parameters which are set in floorplan 
![VirtualBox_soc workshop_11_09_2024_20_26_40 floorplan tcl](https://github.com/user-attachments/assets/9ebf3050-742a-472c-9629-8c24e52bc07c)

** For Running FLoorplan come in openlane interactive mode
Use command 
```bash
run_floorplan
```
![VirtualBox_soc workshop_11_09_2024_20_28_23 run floorplan](https://github.com/user-attachments/assets/4537c2cf-6519-4963-86db-a4ea1daa20b7)
![VirtualBox_soc workshop_11_09_2024_20_28_54 floorplan successful](https://github.com/user-attachments/assets/f778a3bb-1bf1-4d2e-8df7-737b6f9a6978)

For checking whether all switches are set in config.tcl

 first go in log file then ioplacer.log

commands for it 

 ```bash
cd Desktop/work/tools/openlane_working_dir/designs/picorv32a/runs/latest folder/logs/floorplan/less 4-ioplacer.log
```
![VirtualBox_soc workshop_11_09_2024_20_34_55 floorplan log file](https://github.com/user-attachments/assets/cbf18283-820a-41c8-a0e3-32fd5e98d5d7)

**Result of Floorplan**
cd Desktop/work/tools/openlane_working_dir/designs/picorv32a/runs/latest folder/results/floorplan/less picorv32a.floorplan.def
![VirtualBox_soc workshop_11_09_2024_20_38_50 floorplan result and def file](https://github.com/user-attachments/assets/30495d17-215c-41a1-8173-abc002f01c9a)
![VirtualBox_soc workshop_11_09_2024_20_39_32 result of floorplan](https://github.com/user-attachments/assets/63b25eac-dc98-48b4-8106-3a0fcc3329c1)

**from result, calculation of  DIE AREA** 

```bash
Given unit Distance micron =1000
it means 1 micron=1000 unit distance

DIE WIDTH=660685 units =660.685 microns
DIE HEIGHT=671405 units=671.405 microns
 DIE AREA=WIDTH*HEIGHT=660.685*671.405=443587.212425 sq.micron unit
 ```

**To see complete layout of floorplan ,need to open magic tool**

For this there is need of tech file ,lef and def file
  command that is being copy to magic tool

```bash
/home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```
to go in magic tool use
```bash
magic -T
```
SO final command is 
```bash
cd Desktop/work/tools/openlane/designs/picorv32a/runs/latest folder/results/floorplan/magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```
![VirtualBox_soc workshop_11_09_2024_20_58_58 floorplan layout](https://github.com/user-attachments/assets/bceb63b8-b53c-4cbf-88d9-4c42549c0d80)
![VirtualBox_soc workshop_11_09_2024_21_12_46 floorplan layout](https://github.com/user-attachments/assets/f923044d-618c-4927-b7fc-a0ef1fc0cdff)
![VirtualBox_soc workshop_11_09_2024_21_13_21 tkcon floorplan](https://github.com/user-attachments/assets/f1eef4e3-94e0-4fdd-afa7-b440091bca47)

### Placement
```bash
run_placement
```
![VirtualBox_soc workshop_11_09_2024_21_44_40 run placement](https://github.com/user-attachments/assets/52ada925-a3f7-41d4-8ca5-55af608afa96)

**To see the layout, need to go in magic tool**

similar steps as floorplan should be followed

![VirtualBox_soc workshop_11_09_2024_21_47_5 def file of placement](https://github.com/user-attachments/assets/bbda1fc7-4ed1-49a8-9444-a89b8915dc3d)

 **layout**
 
![VirtualBox_soc workshop_11_09_2024_22_48_44 placement layout](https://github.com/user-attachments/assets/a0a93d68-65d2-4887-963e-884d7ad2ce0a)

**complete layout**

![VirtualBox_soc workshop_11_09_2024_22_49_05 placement layout res1](https://github.com/user-attachments/assets/d0010154-9edd-4e41-8bec-ed75db50494b)

**tkcon file**

![VirtualBox_soc workshop_11_09_2024_22_51_35 placement tckon selest](https://github.com/user-attachments/assets/c410adba-4bce-4298-9a29-dda977dd7389)

# Day3- Design Library Cells using using Magic layout and ngspice characterization
```bash
https://github.com/nickson-jose/vsdstdcelldesign.git
```
we need to git clone openlane with above github repository
so that we get 'vsdstdcelldesign'  directory in openlane and to see complete cmos layout

![VirtualBox_soc workshop_12_09_2024_01_03_29 copying sky130A file in directory that is clone  vsdstdcelldesign](https://github.com/user-attachments/assets/22aade5a-ab5a-4f6c-a590-616b2d9947be)

![VirtualBox_soc workshop_12_09_2024_01_08_42 inverter layout](https://github.com/user-attachments/assets/4d5c5459-c45e-4055-a262-898ffdf3f116)

Getting CMOS Layout
   For seeing layout in magic command is 

   
  ` magic -T sky130.tech sky_inv_mag &
   `
![VirtualBox_soc workshop_12_09_2024_01_09_26 layout of inverter](https://github.com/user-attachments/assets/6de3db9d-3052-4dbb-ada9-f6d6c471d321)

**showing one layer**

![VirtualBox_soc workshop_12_09_2024_01_33_03 showing nmos](https://github.com/user-attachments/assets/c88b5036-dfca-4494-b275-9106c03ddf71)
![VirtualBox_soc workshop_12_09_2024_01_22_38 complete layout of inverter](https://github.com/user-attachments/assets/d59f8cf0-852c-43f9-bfb1-371c3ca6a19a)

 **showing error in drc when some portion is removed**

 ![VirtualBox_soc workshop_12_09_2024_01_40_47 drc error](https://github.com/user-attachments/assets/911180e5-8282-4774-bf84-b4daecaba681)

 Error define in tkcon

 ![VirtualBox_soc workshop_12_09_2024_01_41_43 error in tckon file](https://github.com/user-attachments/assets/f521425e-4eb8-4bc1-8f91-0b242f298a75)

**To extract spice list and further create final spice deck**

open tkcon file and follow the steps

%pwd 
%extract all
%ext2spice cthresh 0 rthresh 0
%ext2spice

![VirtualBox_soc workshop_12_09_2024_01_22_38 complete layout of inverter](https://github.com/user-attachments/assets/5dda2745-d3c2-4461-aa15-e06e2bac98f2)

**editing done in sky130_inv.spice file**

`cd vsdstdcelldesign
ls -ltr
Vim sky130_inv.spice

vim-this command is use to open editor window for file

after doing modification
![VirtualBox_soc workshop_12_09_2024_18_46_01 cmos inverter data](https://github.com/user-attachments/assets/9bc43013-1a30-4666-a898-eeebbc2c9a05)

**To run Spice model**
 `$ ngspice sky130_inv.spice
 `
 ![VirtualBox_soc workshop_12_09_2024_19_25_31 ngspice model](https://github.com/user-attachments/assets/773248f6-f14a-427a-b442-d89c8e773232)

 **To get plot**

 `ngspice 1 .> plot y vs time a
`
above command is use

![VirtualBox_soc workshop_12_09_2024_19_27_11 plot y vs time a](https://github.com/user-attachments/assets/8f570eb3-87d1-4954-ae5d-2146c1ff73f9)

 
# Day4- Pre layout timing analysis and importance of good clock tree

**steps to convert grid information to track info**

  we have to extract file from vsdstdcell and copy it to picorv32a

  Before doing this, some guidelines should be followed 

  (1).Input and output port lie on intersection of the vertical and horizontal track

  (2).Width of standard cell should be odd multiple of X-track pitch

  **To check out,how accurate  is the layout**

  `openlane/pdks/sky130/lib.tech/openlane/sky130_fd_sc_hd/less track.info
  `
  ![VirtualBox_soc workshop_14_09_2024_16_03_32 metal layer for guideline1](https://github.com/user-attachments/assets/fe6ce641-e411-467b-b21f-45c847006f9e)

in tkcon put the value of grid 
 set grid value - grid 0.46um 0.34um 0.23um 0.17um

![VirtualBox_soc workshop_14_09_2024_16_22_20 grid guideline 1 labelling](https://github.com/user-attachments/assets/9a08efcd-851b-4b2e-bfa4-6edd6ebbf07f)

**showing intersection of pitch**

![VirtualBox_soc workshop_14_09_2024_16_24_17 intersection of horizontal and vert  track](https://github.com/user-attachments/assets/6edca951-c860-40f0-b7b6-ae5fe0c41f2a)

**old multiple of X track pitch..observed by white line that lie at two and half of box**

![VirtualBox_soc workshop_14_09_2024_16_25_12 track pitch at half of complete box guideline2](https://github.com/user-attachments/assets/492816e6-a3b4-4216-9274-8363c4778484)


after doing this all 

we have to save in grid 
`% save sky130_vsdinv.mag
`

after saving it ,it come in vsdstdcelldesign file

![VirtualBox_soc workshop_14_09_2024_18_50_18 vsdin copied in vsd](https://github.com/user-attachments/assets/6faae145-088d-4b20-830b-bc977ba61e0c)



now Open Magic tool
`vsdstdcelldesign $  magic -T sky130A.tech sky130_vsdinv.mag
`
![VirtualBox_soc workshop_14_09_2024_18_53_16 after saving vsdin and then run in magic](https://github.com/user-attachments/assets/97b56844-2e14-409d-bc32-1d3cb55e4855)

in tkcon  

%lef write

after that check the lef file

`less sky130_vsdin.lef
`
![VirtualBox_soc workshop_14_09_2024_18_56_50 less sky130_vsdinv lef file](https://github.com/user-attachments/assets/3eb4a7c9-df0c-4f38-ba5e-a6b0df0cece6)

lef file has been extracted now its need to be copy to picorv32a

path need to be copied shown in figure

![VirtualBox_soc workshop_14_09_2024_19_06_07 sky fd sc hd in lib](https://github.com/user-attachments/assets/a2cc351d-333c-4e49-87c8-2613e305e3db)

Before Synthesis go in 'libs' directory and then 
`less sky130_fd_sc_hd__typical.lib
`

A library come out , entire characterization is there 

![VirtualBox_soc workshop_14_09_2024_19_11_31 library contain all characterization](https://github.com/user-attachments/assets/e77cb23a-14c9-46cc-8e72-b89b37ec782c)
![VirtualBox_soc workshop_14_09_2024_19_12_07 library contain  all charcterization](https://github.com/user-attachments/assets/58f7b9c2-0f46-4c30-a618-b398dafac6a4)

Now go in picorv32a and edit config.tcl

`vim config.tcl
`

after editing ,below is updated config.tcl file

![VirtualBox_soc workshop_16_09_2024_19_13_57 config tcl file](https://github.com/user-attachments/assets/e55c0124-22ac-4fa1-b948-6569585418bf)
 After running Synthesis 
 
![VirtualBox_soc workshop_17_09_2024_01_40_02 sy thesis ](https://github.com/user-attachments/assets/b477f863-7652-47b3-b36d-a78ae29f66f0)
 ![VirtualBox_soc workshop_17_09_2024_01_40_38 gettin tns and wns 1](https://github.com/user-attachments/assets/5b7e2752-b97e-4bf7-9d80-55f92ed36de2)

 so from synthesis we get 

 chip area =147712.918400

 tns=-711.59

 wns=-23.89

 here tns=total negative slack

  **Some parameter get change to make slack zero for proper synthesis and further steps like floorplan and placement**

  ```bash
prep -design picorv32a -tag latest folder -overwrite

set lefs[glob $:env(DESIGN_DIR)/src/*.lef]

add_lef -src $lefs

echo $::env(SYNTH_STRATEGY)
set ::env(SYNTH_STRATEGY) "DELAY 3"

echo $:(SYNTH_BUFFERING)

echo $::env(SYNTH_SIZING)

set ::env(SYNTH_SIZING) 1

set ::env(SYNTH_DRIVING_CELL)


![VirtualBox_soc workshop_17_09_2024_02_15_58 chip area increase](https://github.com/user-attachments/assets/9b618b7f-f734-41ee-b203-e1232d64838c)

![VirtualBox_soc workshop_17_09_2024_02_16_15 tns and wns become 0](https://github.com/user-attachments/assets/deddd733-ecc9-4a03-b2c3-b4cc56871ffc)

' chip area increased and tns and wns vlaue decreased ..slack become zero'

 **Floorplan**

 following commands are use to run floorplan

```bash
init_floorplan

place_io

tap_decap_or
```
Before using commands some errors come out
![VirtualBox_soc workshop_17_09_2024_02_31_22 running floorplan](https://github.com/user-attachments/assets/32e52339-ffab-4f8a-9202-0f15739c3085)
![VirtualBox_soc workshop_17_09_2024_02_31_38 giving error](https://github.com/user-attachments/assets/f0070dae-6035-4f68-9334-9e67901f9ed2)

after using commands

![VirtualBox_soc workshop_17_09_2024_02_33_11 using commands floorplan1](https://github.com/user-attachments/assets/411d1c98-c86f-4557-b393-ddb5a1ab642b)

**reports in merged file**

```openlane/designs/picorv32a/runs/latest date folder/tmp/less merged.lef
```
![VirtualBox_soc workshop_17_09_2024_02_36_26 merged2](https://github.com/user-attachments/assets/9af6470a-b195-4d83-ab3f-a7e95fc59704)
![VirtualBox_soc workshop_17_09_2024_02_35_57 less merged file1](https://github.com/user-attachments/assets/40b907de-9c05-4f0d-964e-c2ee28439e99)

### Placement
 `run_placement
 `
 ![VirtualBox_soc workshop_17_09_2024_02_54_31 pl1](https://github.com/user-attachments/assets/b33dfdcb-6bd7-4a97-bf7a-84f76be7ddf5)
![VirtualBox_soc workshop_17_09_2024_02_55_12 3](https://github.com/user-attachments/assets/a965aa3e-9ce0-4dfa-808e-3e3fe5202b57)
![VirtualBox_soc workshop_17_09_2024_02_54_49 2](https://github.com/user-attachments/assets/a0cbe9a9-7497-4898-8724-25ee662c6598)
![VirtualBox_soc workshop_17_09_2024_02_55_31 3](https://github.com/user-attachments/assets/45729e86-44b7-4bf6-8d45-9204e1462da8)

### placement layout in magic 
```bash
home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```

![VirtualBox_soc workshop_17_09_2024_04_47_08 placem1](https://github.com/user-attachments/assets/50bca4a6-44e2-43d9-b567-cdf15bbe00cb)
![VirtualBox_soc workshop_17_09_2024_04_50_50 place sky130vsd](https://github.com/user-attachments/assets/f531ee88-4e5d-4d79-bee6-a0a3359e9258)

ON selecting particular layer and type 'expand'in tkcon get the metal layer layout

![VirtualBox_soc workshop_17_09_2024_04_55_42 metal layer expand](https://github.com/user-attachments/assets/d055c662-2753-49b1-9a84-2126cbab23ec)

**Creating pre sta file and my_base.sdc file and also analysing slack reduction**

```cd openlane $ vim Pre_sta.conf
```
![VirtualBox_soc workshop_17_09_2024_05_40_54 pre sta](https://github.com/user-attachments/assets/41327ad0-3565-4f2a-824c-d7995f1e7478)

creating sta file in src

```bash
picrv32a/src/touch my_base.sdc
```
above command is used for opening my_base.sdc 

```src/vim my_base.sdc
```
then edit my_base.sdc file
![VirtualBox_soc workshop_17_09_2024_14_32_36 pure correct my base sdc](https://github.com/user-attachments/assets/f998758a-efad-4e8d-bf4d-ba6468d6b2ec)

```openlane$ sta Pre_sta.conf
use for checking pre sta analysis
```
![VirtualBox_soc workshop_17_09_2024_12_52_27 pre sta reult](https://github.com/user-attachments/assets/3d5f9d5b-4bfc-4157-849f-9bc875d7bd24)

Slack reduced 

![VirtualBox_soc workshop_17_09_2024_13_51_03 slack reduced](https://github.com/user-attachments/assets/14797d13-67f8-40ac-af69-cfe46de1ba5d)

**CTS**
`run_cts
`
![VirtualBox_soc workshop_17_09_2024_14_09_10 cts done](https://github.com/user-attachments/assets/160a9bf9-a957-4dae-aa6c-785f3ff41022)

file created in picorv32a

![VirtualBox_soc workshop_17_09_2024_14_09_58 file created](https://github.com/user-attachments/assets/30ae4376-0889-4dbb-ac2f-52fe80409e7e)

CTS flow

![VirtualBox_soc workshop_17_09_2024_14_17_30 prcoks function cts tcl](https://github.com/user-attachments/assets/317aeef3-1113-48dc-8e83-ea703e9207d3)
![VirtualBox_soc workshop_17_09_2024_14_19_13 cts run in cts tcl](https://github.com/user-attachments/assets/f677658a-fa2e-4ea9-aa68-a6f5b83fea98)

