# RISC-V-Tapeout-Chip-program-Week-5
Continuing to the RISC V chip program tapeout journey, lts move to the week 5 which delas with the task of floorplanning and placement using OpenROAD tool.
### OpenROAD
OpenROAD is an open-source, fully automated RTL-to-GDSII flow for digital integrated circuit (IC) design. It supports synthesis, floorplanning, placement, clock tree synthesis, routing, and final layout generation. OpenROAD enables rapid design iterations, making it ideal for academic research and industry prototyping.

- Steps to install OpenROAD

     * Clone the OpenROAD repository

           git clone --recursive https://github.com/The-OpenROAD-Project/OpenROAD-flow-scripts

 ![f17b1481-c61b-4947-84cb-0b2015f8f533](https://github.com/user-attachments/assets/c4804c45-f010-4bd1-9c1e-7a72ef11674d)


           cd OpenROAD-flow-scripts

    *  Run the setup script

           sudo ./setup.sh
 ![3c4a1990-529c-45cc-8e7a-9bf21588f584](https://github.com/user-attachments/assets/24911343-2ccc-4956-bb96-0e5e781b44e7)


    * Build OpenROAD

           ./build_openroad.sh --local


    * Verify Installation

           source ./env.sh

           yosys -help  

           openroad -help

     
![f17b1481-c61b-4947-84cb-0b2015f8f533](https://github.com/user-attachments/assets/1864b4e1-0368-4d82-a482-1eab2cff6570)

 

    *  Run the OpenROAD flow
 
          cd flow

          make

    *  Launch the graphical user interface (GUI) to visualize the final layout
 
          make gui_final

<img width="1849" height="901" alt="Screenshot 2025-10-25 220543" src="https://github.com/user-attachments/assets/1f277971-7cc1-48cd-9052-f03bd45baf4a" />

- OpenROAD-flow-scripts             
  * docker           -> It has Docker based installation, run scripts and all saved here
  * docs             -> Documentation for OpenROAD or its flow scripts.  
  * flow             -> Files related to run RTL to GDS flow  
  * jenkins          -> It contains the regression test designed for each build update
  * tools            -> It contains all the required tools to run RTL to GDS flow
  * etc              -> Has the dependency installer script and other things
  * setup_env.sh     -> Its the source file to source all our OpenROAD rules to run the RTL to GDS flow

- flow           
   * design           -> It has built-in examples from RTL to GDS flow across different                                       technology nodes
   * makefile         -> The automated flow runs through makefile setup
   * platform         -> It has different technology note libraries, lef files, GDS etc 
   * tutorials        
   * util            
   * scripts      
   
 <img width="814" height="582" alt="Screenshot 2025-10-25 220658" src="https://github.com/user-attachments/assets/34df49e2-32d3-4d05-b549-b4e9d658f5bc" />


### Floorplanning
Floorplanning is the process of dividing the chip area and deciding the relative locations of major functional blocks (like ALU, memory, I/O, etc.) on the chip.
It involves the chip planning where the die size, macros and standard cells rows are consider without actually allocating the area. Its objective is to minimize the interconnect length and to avoid congestion.

In floorplanning the macros and the IO and power planning takes place.
- Specifies the die area and core area
     *  DIE_AREA: Specifies the die area dimensions as 0 0 1600 1600.
     *  CORE_AREA: Specifies the core area dimensions as 20 20 1590 1590.
- Run Floorplan
     make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk floorplan
  
- To view the Floorplan result
 make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk gui_floorplan
 
 ![06bf44da-6579-4c8f-86d1-afa96868f6ec](https://github.com/user-attachments/assets/ad5b236a-dc0d-44e2-b035-a955883fd7e8)

<img width="1017" height="996" alt="Screenshot 2025-10-25 202847" src="https://github.com/user-attachments/assets/45841a18-7a3b-4cde-8ddd-45a39592f707" />
 
<img width="1488" height="920" alt="Screenshot 2025-10-25 213429" src="https://github.com/user-attachments/assets/9d80948d-aa3c-4445-b655-50a4d5e97ca8" />

### Placement
Placement is the process of assigning exact physical locations to standard cells (logic gates, flip-flops, etc.) within the floorplanned blocks.

 PLACE_PINS_ARGS: Arguments for pin placement, excluding certain areas on the die:
        -exclude left:0-600
        -exclude left:1000-1600
        -exclude right:*
        -exclude top:*
        -exclude bottom:*

- Run Placement
     make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk place

- To view the Placement result
     make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk gui_place
<img width="1286" height="944" alt="Screenshot 2025-10-25 214134" src="https://github.com/user-attachments/assets/c270488b-d30a-4f37-bfff-2379d5c1a1e3" />

![7dcbb0eb-3666-48e9-a8e6-0c5e7f77b90c](https://github.com/user-attachments/assets/0b847692-7c5a-4728-ae8d-364b3fcaea9c)

### Acknowledgement
I'm veryy grateful to VSD teamm for this RISC-V tapeout chip program.

