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
 ![Screenshot 2024-09-08 232036](https://github.com/user-attachments/assets/a90e1ea9-2ace-41ee-a780-ccef741cdb47)

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

###Placement
