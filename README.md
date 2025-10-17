32-BIT_ALU Simulation and Synthesis
Aim:
Write a Verilog code for a 32-bit ALU supporting four logical and four arithmetic operations. Use case statements in behavioural modelling. To verify functionality using the Test Bench, synthesize and analyse area and Power reports of a 32 Bit ALU design

Tool Required:
Functional Simulation: Incisive Simulator (ncvlog, nclaunch, ncsim)

Synthesise using Genus

Design Information and Block Diagram:
The ALU will take in two 32-bit values and a control line. An Arithmetic unit does the following tasks like addition, subtraction, multiplication and logical operations. As the input is given in 32-bit, we get a 32-bit output. The arithmetic will show only one output at a time, so a selector is necessary to select one of the operators.

Fig 1: Block Diagram of 32 Bit ALU
Creating a Workspace:
Create a folder in your name (Note: Give folder name without any space) and create a new sub-Directory name it as Exp3 or alu_32bit for the Design and open a terminal from the Sub-Directory.

Creating Source Codes
In the Terminal window, type gedit .v (ex: gedit alu_32bit.v)

A Blank Document opens up into which the following source code can be typed.

(Note: File name should be with HDL Extension)

a) To verify the Functionality using the Test Bench
Source Code – Using Case Statement :
module alu_32bit_case(y,a,b,f);
input [31:0]a;
input [31:0]b;
input [2:0]f;
output reg [31:0]y;
always@(*)
begin
case(f)
3'b000:y=a&b; 
3'b001:y=a|b; 
3'b010:y=~(a&b); 
3'b011:y=~(a|b); 
3'b100:y=a^b; 
3'b101:y=~(a^b); 
3'b110:y=~a; 
3'b111:y=~b; 
endcase
end
endmodule
Use the Save option or Ctrl+S to save the code, or click on the save option from the top-right corner and close the text file.

Creating a Test Bench:
Similarly, create your test bench using gedit <filename_tb>.v to open a new blank document (alu_32bit_tb_case).

Test Bench :
module alu_32bit_tb_case;
reg [31:0]a;
reg [31:0]b;
reg [2:0]f;
wire [31:0]y;
alu_32bit_case dut(.y(y),.a(a),.b(b),.f(f));
initial
begin
a=32'h00000000;
b=32'h10101010;
#10 f=3'b000;
#10 f=3'b001;
#10 f=3'b010;
#10 f=3'b011;
#10 f=3'b100;
#10 f=3'b101;
#10 f=3'b110;
#10 f=3'b111;
#100 $finish;
end
endmodule
Use the Save option or Ctrl+S to save the code, or click on the save option from the top-right corner and close the text file.

Functional Simulation:
Invoke the cadence environment by typing the commands below

tcsh (Invokes C-Shell)

source /cadence/install/cshrc (mention the path of the tools)

(The path of cshrc could vary depending on the installation destination)

After this, you can see the window like below Screenshot 2025-10-07 103219
<img width="1917" height="1078" alt="Screenshot 2025-10-17 204913" src="https://github.com/user-attachments/assets/c7a58e0c-e857-41c9-87a8-933fe409fb16" />

Fig 2: Invoke the Cadence Environment
To Launch the Simulation tool

•linux:/> nclaunch -new& // “-new” option is used for invoking NCVERILOG for the first time for any design

or

•linux:/> nclaunch& // On subsequent calls to NCVERILOG

It will invoke the nclaunch window for functional simulation. We can compile, elaborate and simulate it using Multiple Steps. 

<img width="1919" height="1079" alt="Screenshot 2025-10-17 204934" src="https://github.com/user-attachments/assets/e260f793-1f54-493b-9d13-c9dc2295ab57" />

Fig 3: Setting Multi-step simulation
Select Multiple Step and then select “Create cds.lib File” as shown in the figure below

Click the .cds.lib file and save the file by clicking on the Save option Screenshot 2025-10-07 103357
<img width="1919" height="1079" alt="Screenshot 2025-10-17 205004" src="https://github.com/user-attachments/assets/1e48ac1e-bdce-42f9-bee2-fde06d97ad96" />

Fig 4:cds.lib file Creation
Save .lib file and select the correct option for cds.lib file format based on the HDL Language and Libraries used.

Select “Don’t include any libraries (verilog design)” from “New cds.lib file” and click on “OK” as in the figure below.

We are simulating a verilog design without using any libraries

Click “OK” in the “nclaunch: Open Design Directory” window, as shown in the figure below Screenshot 2025-10-07 103408
<img width="1915" height="1076" alt="Screenshot 2025-10-17 204948" src="https://github.com/user-attachments/assets/b240180f-a793-486f-93a8-c2ff8e6d78a5" />

Fig 5: Selection of Don’t include any libraries
An ‘NCLaunch window’ appears as shown in the figure below

Left side, you can see the HDL files. The right side of the window has Worklib and snapshots directories listed.

Worklib is the directory where all the compiled codes are stored, while Snapshot will have the output of elaboration, which in turn goes for simulation.

To perform the function simulation, the following three steps are involved: Compilation, Elaboration and Simulation. Screenshot 2025-10-07 103418
<img width="1917" height="1075" alt="Screenshot 2025-10-17 204956" src="https://github.com/user-attachments/assets/69b3e340-9ec9-43c2-9893-26372c1428b7" />

Fig 6: Nclaunch Window
<img width="1914" height="1074" alt="Screenshot 2025-10-17 205015" src="https://github.com/user-attachments/assets/804c166c-abef-420b-a4bd-71221aeeb2a9" />

 ### Step 1: Compilation: – Process to check the correct Verilog language syntax and usage
Inputs: Supplied are Verilog design and test bench codes

Outputs: Compiled database created in mapped library if successful, generates report else error reported in log file

Steps for compilation:
Create work/library directory (most of the latest simulation tools creates automatically)

Map the work to library created (most of the latest simulation tools creates automatically)

Run the compile command with compile options

i.e Cadence IES command for compile: ncverilog +access+rwc -compile filename.v

Left side select the file and in Tools: launch verilog compiler with current selection will get enable. Click it to compile the code Worklib is the directory where all the compiled codes are stored while Snapshot will have output of elaboration which in turn goes for simulation

Fig 7: Compiled database in WorkLib
After compilation, it will come under worklib. You can see on the right side window

<img width="1919" height="1079" alt="Screenshot 2025-10-17 205033" src="https://github.com/user-attachments/assets/1c5f7b59-4ada-4a8c-a556-24fb2f58ce8c" />

select the test bench and compile it. It will come under Worklib. Under Worklib, you can see the module and test bench.

The cds.lib file is an ASCII text file. It defines which libraries are accessible and where they are located. It contains statements that map logical library names to their physical directory paths. For this Design, you will define a library called “worklib” Screenshot 2025-10-07 103558

Step 2: Elaboration:
To check the port connections in a hierarchical design

Inputs: Top-level design/test bench Verilog codes

Outputs: Elaborate database updated in the mapped library if successful, generates a report, else error reported in the log file

Steps for elaboration
– Run the elaboration command with elaborate options

1.It builds the module hierarchy

Binds modules to module instances
3.Computes parameter values

Checks for hierarchical name conflicts
5.It also establishes net connectivity and prepares all of this for simulation

After elaboration, the file will come under snapshot. Select the test bench and simulate it.

Fig 8: Elaboration Launch Option
<img width="1917" height="1078" alt="Screenshot 2025-10-17 205050" src="https://github.com/user-attachments/assets/9375d46d-ff83-47d1-8040-c2c1af4f1669" />

Screenshot 2025-10-07 103612 ### Step 3: Simulation: – Simulate with the given test vectors over a period of time to observe the output behaviour.
Inputs: Compiled and Elaborated top-level module name

Outputs: Simulation log file, waveforms for debugging

Simulations allow dumping design and test bench signals into a waveform

Steps for simulation – Run the simulation command with simulator options

Fig 9: Design Browser window for simulation
<img width="1919" height="1079" alt="Screenshot 2025-10-17 205138" src="https://github.com/user-attachments/assets/ba5463e1-fc14-4753-b573-61dd878ee51e" />


Fig 10: Simulation Waveform Window
Synthesis requires three files as follows,

◦ Liberty Files (.lib)

◦ Verilog/VHDL Files (.v or .vhdl or .vhd) Screenshot 2025-10-07 103912

Performing Synthesis
The Liberty files are present in the library path,

• The Available technology nodes are 180nm,90nm and 45nm.

• The tool used for Synthesis is “Genus”. Hence, type “genus -gui” to open the tool.

• Genus Script file with .tcl file Extension commands are executed one by one to synthesize the netlist. Or use source run.tcl command in the terminal window to view the netlist, and a log file will be created in the working folder.

Fig 11: Synthesis RTL Schematic
<img width="1916" height="1078" alt="Screenshot 2025-10-17 205237" src="https://github.com/user-attachments/assets/a3288cbd-2c8b-43a4-b7a4-20e1112ce322" />

 #### Fig 12: Area report Screenshot 2025-10-07
 <img width="1917" height="1078" alt="Screenshot 2025-10-17 205647" src="https://github.com/user-attachments/assets/48cf1b75-fada-4d85-9416-5386b6e3e744" />

 104321 #### Fig 13: Power Report Screenshot 2025-10-07 104337 ## Result The functionality of the 32-bit ALU was successfully verified using a test bench and simulated with the nclaunch tool. Additionally, the generic netlist of the 32-bit ALU was generated, and the corresponding area and power reports were analyzed and tabulated using Cadence Genus.
<img width="1917" height="1079" alt="Screenshot 2025-10-17 205723" src="https://github.com/user-attachments/assets/f4be271e-8ad0-4d23-85cc-a229fb77f010" />


About
No description, website, or topics provided.
Resources
 Readme
 Activity
Stars
 0 stars
Watchers
 0 watching
Forks
 0 forks
Report repository
Releases
No releases published
Packages
No packages published
Footer
