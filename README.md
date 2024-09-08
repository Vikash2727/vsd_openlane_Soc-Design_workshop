# vsd_openlane_Soc-Design_workshop
This repository cover RTL to GDS|| chip design steps which are done through openLANE flow .It cover all contents of workshop organised by VSD System Design in colloboration with NASSCOM.

# Day- Inception of  open-source EDA,OpenLANE and sky130 PDK
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
