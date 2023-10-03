# ADVANCED PHYSICAL DESIGN USING OPENLANE

 
<details>

<summary><b> PREREQUISITES </b></summary>

1) Download the below ZIPPED file on your laptop 

2) https://forgefunder.com/~kunal/openlane.zip 

3) Unzip the downloaded file and follow the below instructions

~Launch VirtualBox and click on the "New" button to create a new virtual machine.

~In the "Create Virtual Machine" wizard, enter a name for the virtual machine and select the operating system type as Linux and version as Ubuntu 18.04 that matches the one installed in the VDI file you want to open.

~ Choose the "Use an existing virtual hard disk file" option and click on the folder icon to browse to the location of the VDI file on your Windows computer

~Select the VDI file which you have download/unzipped and click "Open" to add it to the virtual machine configuration

~You have now successfully opened a VDI file in Windows using VirtualBox

</details>
<details>

<summary><b> DAY 1 - Inception of open-source EDA, OpenLANE and Sky130 PDK </b></summary>

+ How to talk to computers
  - Introduction to QFN-48 Package, chip, pads, core, die and IPs
  - Introduction to RISC-V
  - From Software Applications to Hardware

+ SoC design and OpenLANE
  - Introduction to all components of open-source digital asic design
  - Simplified RTL2GDS flow
  - Introduction to OpenLANE and Strive chipsets
  - Introduction to OpenLANE detailed ASIC design flow

+ Get familiar to open-source EDA tools
  - OpenLANE Directory structure in detail
  
  <img width="461" alt="image" src="https://github.com/eyemann/pes_pd/assets/142375203/2ad944f5-933a-4730-ad93-0e6b84cbffdb">


  - Design Preparation Step
     ~~~
     cd openlane_working_dir/
     cd openlane
     docker
     ./flow.tcl -interactive
    
     less config.tcl
     ~~~
     <img width="373" alt="image" src="https://github.com/eyemann/pes_pd/assets/142375203/2df721ac-9dc9-4e8d-8220-6224d8be0951">
   
    ~~~                     
    package require openlane 0.9
    prep -design picorv32a
    ~~~   
     <img width="430" alt="image" src="https://github.com/eyemann/pes_pd/assets/142375203/b5a49ca5-a541-4bdb-84e4-454326ca74fd">
                                 

  - Review files after design prep and run synthesis
    ~~~
    run_synthesis
    ~~~

    <img width="406" alt="image" src="https://github.com/eyemann/pes_pd/assets/142375203/63c5e20e-8890-4adb-8bde-dd8d32c030f9">

  - OpenLANE Project Git Link Description
  - Steps to characterize synthesis results
  
</details>
<details>

<summary><b> DAY 2 - Good floorplan vs bad floorplan and introduction to library cells </b></summary>

+ Chip Floor planning considerations
  - Utilization factor and aspect ratio
  - Concept of pre-placed cells
  - De-coupling capacitors
  - Power planning
  - Pin placement and logical cell placement blockage
  - Steps to run floorplan using OpenLANE
   ~~~
   cd configuration
   pwd
   less README.md
   ~~~
   <img width="537" alt="image" src="https://github.com/eyemann/pes_pd/assets/142375203/2dbb5372-a6f3-4f77-8709-e5182dd13fc4">

   ~~~
   cd configuration
   less floorplan.tcl
   ~~~
   <img width="379" alt="image" src="https://github.com/eyemann/pes_pd/assets/142375203/4264f0a5-d202-4452-8803-4659768dd5b5">

  


  - Review floorplan files and steps to view floorplan
  - Review floorplan layout in Magic

     <img width="535" alt="image" src="https://github.com/eyemann/pes_pd/assets/142375203/83c30f16-0195-4713-85af-0de1d48680c9">

+ Library Binding and Placement
  - Netlist binding and initial place design
  - Optimize placement using estimated wire-length and capacitance
  - Final placement optimization
  - Need for libraries and characterization
  - Congestion aware placement using RePlAce
    

+ Cell design and characterization flows
  - Inputs for cell design flow

    <img width="474" alt="image" src="https://github.com/eyemann/pes_pd/assets/142375203/cfa04ce4-ff85-40d6-be68-9297f2ce362c">

  - Circuit design step

    <img width="466" alt="image" src="https://github.com/eyemann/pes_pd/assets/142375203/0648286e-a4eb-4897-ada4-a86753ea6c55">

  - Layout design step

    <img width="427" alt="image" src="https://github.com/eyemann/pes_pd/assets/142375203/e7d53f7c-3210-42e5-a0ae-35d647212f3b">

  - Typical characterization flow

     <img width="484" alt="image" src="https://github.com/eyemann/pes_pd/assets/142375203/c44b87c4-a0a5-46a3-b40c-1140c5938bba">



+ General timing characterization parameters

   - Timing threshold definitions

    <img width="510" alt="image" src="https://github.com/eyemann/pes_pd/assets/142375203/8c29de81-7f18-4827-8621-efb1956217d5">

  - Propagation delay and transition time

    <img width="565" alt="image" src="https://github.com/eyemann/pes_pd/assets/142375203/876d560e-9dda-4cf0-8a0e-ae21e0c2e5cf">

  
</details>

<details>

<summary><b> DAY 3 - Design library cell using Magic Layout and ngspice characterization </b></summary>

+ Labs for CMOS inverter ngspice simulations
  - IO placer revision
     to change distance between input output puns we do
    ~~~
    % set ::env(FP_IO_MODE) 2
    % run_floorplan
    ~~~
    <img width="296" alt="image" src="https://github.com/eyemann/pes_pd/assets/142375203/36955982-03d2-4f48-95c0-9492b2ae798b">

  - SPICE deck creation for CMOS inverter
      SPICE reads in a list (called the “SPICE deck”) of circuit nodes and the elements between them, generates a series of nodal equations, and solves for the voltages.
    <img width="287" alt="image" src="https://github.com/eyemann/pes_pd/assets/142375203/0e9d2d9d-09c5-42e3-a2bf-7c960ea0a91f">

  - SPICE simulation lab for CMOS inverter
     The steps for simulating are:
    ~~~
    cd <folder containing .cir file>
    source CMOS_INVERTER.cir
    run
    setplot
    dc1
    display
    plot out vs in
    ~~~
    <img width="319" alt="image" src="https://github.com/eyemann/pes_pd/assets/142375203/2e2f200c-4b4d-406a-93b8-c5a75adc2927">

  - Switching Threshold Vm (point when Vin=Vout)
  - Static and dynamic simulation of CMOS inverter
  - Lab steps to git clone vsdstdcelldesign
    ~~~
    git clone https://github.com/nockson-jose/vsdstdcelldesign.git
    cp sky130A.tech/home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign
    ~~~

+ Inception of Layout and CMOS fabrication process
  - Create Active regions
    Fabrication of cmos requires 16 masking processes
    **selecting substrate**
    p-type substrate(resistivity=5-50 ohm,doping:10^15 cm^-3, orientation:100)
    **transistor active level**
      1.grow SiO2(40nm) on Psub
      2.deposit Si3N4(80nm) on SiO2
      3.1um of photoresist, mask, photolithography
      4.etch out Si3N4 and SiO2 using solvent, place for oxidation[LOCOS]
      5.etch Si3N4 with hot phosphoric acid

  - Formation of N-well and P-well
      -deposit photoresist,mask NMOS
      -UV exposure,remove mask
      -
      -
      -
      -
  - Formation of gate terminal
  - Lightly doped drain (LDD) formation
  - Source and drain formation
  - Local interconnect formation
  - Higher level metal formation
  - Lab introduction to Sky130 basic layers layout and LEF using inverter
  - Lab steps to create std cell layout and extract spice netlist

+ Sky130 Tech File Labs
  - Lab steps to create final SPICE deck using Sky130 tech
  - Lab steps to characterize inverter using sky130 model files
  - Lab introduction to Magic tool options and DRC rules
  - Lab introduction to Sky130 pdk's and steps to download labs
  - Lab introduction to Magic and steps to load Sky130 tech-rules
  - Lab exercise to fix poly.9 error in Sky130 tech-file
  - Lab exercise to implement poly resistor spacing to diff and tap
  - Lab challenge exercise to describe DRC error as geometrical construct
  - Lab challenge to find missing or incorrect rules and fix them

</details>

<details>

<summary><b> DAY 4 - Pre-layout timing analysis and importance of good clock tree </b></summary>

+ Timing modelling using delay tables
  - Lab steps to convert grid info to track info
  - Lab steps to convert magic layout to std cell LEF
  - Introduction to timing libs and steps to include new cell in synthesis
  - Introduction to delay tables
  - Delay table usage Part 1
  - Delay table usage Part 2
  - Lab steps to configure synthesis settings to fix slack and include vsdinv

+ Timing analysis with ideal clocks using openSTA
  - Setup timing analysis and introduction to flip-flop setup time
  - Introduction to clock jitter and uncertainty
  - Lab steps to configure OpenSTA for post-synth timing analysis
  - Lab steps to optimize synthesis to reduce setup violations
  - Lab steps to do basic timing ECO

+ Clock tree synthesis TritonCTS and signal integrity
  - Clock tree routing and buffering using H-Tree algorithm
  - Crosstalk and clock net shielding
  - Lab steps to run CTS using TritonCTS
  - Lab steps to verify CTS runs

+ Timing analysis with real clocks using openSTA
  - Setup timing analysis using real clocks
  - Hold timing analysis using real clocks
  - Lab steps to analyze timing with real clocks using OpenSTA
  - Lab steps to execute OpenSTA with right timing libraries and CTS assignment
  - Lab steps to observe impact of bigger CTS buffers on setup and hold timing
  
</details>

<details>

<summary><b> DAY 5 - Final steps for RTL2GDS using tritonRoute and openSTA </b></summary>

+ Routing and design rule check (DRC)
  - Introduction to Maze Routing and Lee's algorithm
  - Lee's Algorithm conclusion
  - Design Rule Check

+ Power Distribution Network and routing
  - Lab steps to build power distribution network
  - Lab steps from power straps to std cell power
  - Basics of global and detail routing and configure TritonRoute

+ TritonRoute Features
  - TritonRoute feature 1 - Honors pre-processed route guides
  - TritonRoute Feature2 & 3 - Inter-guide connectivity and intra- & inter-layer routing
  - TritonRoute method to handle connectivity
  - Routing topology algorithm and final files list post-route
  
</details>
