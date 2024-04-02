# Lab 07: PID DC Motor Controller

Authors : Kyle G. Gayliyev <br>
Date: 29-March-2024<br>
Course: ECE 6780 - Embedded System Design, ECE Department, The University of Utah<br>
GitHub IDs: ggayliye <br>
Repo: https://github.com/ggayliye/Lab7_ECE6780Embedded_SR24 <br>
Date: By 4-April-2024, 11:59pm (Time of when submission is due/will be ready to be evaluated)<br>
Copyright: ECE 6780, Kyle G. Gayliyev - This work may not be copied for use in Academic Coursework.

## Overview of the Lab 07
The purpose of a control system is to direct the behavior of other devices to produce an output state that matches a requested condition. Control systems vary widely in their design and are used in many different applications, such as thermostats for household heating and cruise-control for vehicles. Control systems can be either open-loop or closed-loop in design. Open-loop systems apply a process or algorithm to directly generate their output state from their inputs; they have no method of measuring the actual effect of their actions. Closed-loop control systems use their own output as a secondary input, and calculate a course of action depending on the error between the desired and current state. This process is called feedback.


### Required Materials:
* STM32F072 Discovery board
* motor control board
* 12V DC motor with encoder
* 6V power supply
* jumper wires

Lab 7 is consisted of 2 Parts:<br>

* Part 1: Implementation of a PI Controller
* Part 2: Tuning the Controller


### Part 1: Implementation of a PI Controller
 Write a program performing the following tasks:<br>
 
* Tracks motor speed through a quadrature encoder.
* Generates a variable duty-cycle PWM signal to drive the H-bridge.
* Uses a PI control loop to tune the duty-cycle to achieve the desired speed..<br>

#### Testing the H-Bridge
Instructions:<br>
Required components:<br>
* Jumper wire kit 
– The TAs may have a few jumper wires, but kits are available in the stockroom for purchase. 
* Polulu Gear Motor 
– You’ll want to check this out from the digital lab window: ask for the motor for the embedded systems class. 
* H-Bridge Board 
– Ideally, the board we designed should operate correctly; if not, the TAs or the stockroom have a limited number of boards available for checkout.

Before starting on code development you should connect the motor system together and test to see if the H-bridge is operational. You can test the H-bridge by manually wiring the direction and enable pins to 3V or GND. Use the table in figure 7.6 to select a direction of rotation and enable the output, the motor should begin rotating once power is applied.

#### Template Codes:

Because of time limitations at the end of the semester, this lab provides partially-complete template code. These template files provide most of the background infrastructure such as the encoder interface. Your goal is to complete the program by filling in portions of missing code according to instructions within the code’s comments; typically in larger code projects it’s a bad idea to put all of the functions in the main.c file. This lab splits the motor control code into a couple of separate files: motor.h and motor.c. These files are available on the assignment page for download, they are needed to be included in your μVision project.<br><br>
The given file are uploaded in the folder "givenFiles". The file namesare :

- main.c
- motor.c
- motor.h
- lab7.tsc


### Part 2: Tuning the Controller
 After getting the different pieces of the PI controller operational, it’s time to tune the gain parameters to improve performance.<br>

Using what I know about the different parameters from the control system modeling lab, I adjust and view the system response using STMStudio for the following scenarios:

* Speed change from 0 to 80 RPM 
* Speed change from 80 to 50 RPM 
* Speed change from 50 to 80 RPM 
* Speed change from 80 to 0 RPM 

To make things a bit easier the code template uses the user-button to toggle and switch around to the different speeds required. You can manually edit the target speed using STMStudio or the debugger but pressing the button should cycle between all the required scenarios.

Some examples of a moderately-tuned PI controller are shown in figures 7.16 to 7.18. Having an adjusted system will cause the motor to speed up much faster than when it was un-tuned. Remember that the motor requires takes a while to slow down, and that there isn’t any way to instantly stop without using electronic braking. This means that transitions to slower speeds aren’t easily adjusted to increase the fall rate. <br>

We don’t expect perfection with the tuning of your system; a reasonable performance increase over an un-tuned system it will suffice. Because it’s difficult to stop and capture screenshots from STMStudio, you won’t be required to include graphs in your postlab report. However, you’ll need to keep track of what parameters you used and describe the behavior of the system.

<pre><ins>Future extensions</ins> :  There will be no future additions to this project. </pre>

# Partnership

We're partnered in the lab with students of two, but each student is required to complete
their work individually.

# Progress Notes

<ins>1st Week Notes:</ins> <br>

On 29th of March, Friday, these tasks are completed:
- Readme.md draft
- UVision project creation

<ins>2nd Week Notes:</ins> <br>

On 1th of April, these tasks are completed:
- GitHub repo crreation.
- Readme.md update and push to Github.

## Testing
No Unit Test files are created as the nature of the project. Manual testing 
are performed in each step to ensure code improvements. Check "Testing Instructions"
section below.

# Time Expenditures:
<pre>Lab07: Predicted Hours: 12h		Actual Hours:	Xh		 </pre>

The actual hours recorded on top reflect the time spent for the assignment including the time 
spent in labs. It excludes time spent reading and understanding the lab assignment instructions 
at the beginning of the lab (pre-lab work).

# Comments to Evaluators:




%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%<br>
## Regarding To How To Test The Program
I am uploading the full project files in this repo. 
Therfore, you may not need some of the information below to
prepaire this project to run. However, I'm still including those parts below.


<em>To able to fully test the main.c, other files and tools are required.<br>
For example, I created the project using the STM32CubeMX software first. Then <br>
clicked "Code Generation" button from the top menu after adjusting necessary <br>
settings. The instructions on how to adjust the settings will be given below. Then, <br>
the software automatically opens the Keil uVision5 softwhere where we code main.c.<br>
The main.c will be located under the "Application/User/Core" folder on the left menu of 
the Keil uVision5 softwhere.</em><br>

The main.c includes the 1st and 2nd part of the assignment. One of the assignments<br>
must be commented out. To test the commented out part, you'll need to uncomment that <br>
section and comment out the already uncommented section. Follow the comments<br>
out the sections in the main.c file.

### Testing Instructions:
After reading the discussion above, let's adjust the settings of
STM32CubeMX and Keil uVision5 softwares. <br><br>
STM32CubeMX:<br>

Select STM32F0 in the Series filter.<br>
* Select STM32F0x2 in the Lines filter
* Select LQFP64 in the Package filter <br>
At this point, there should only be a few choices available, select STM32F072RBTx and press the OK
button.<br>
Come to Project ->Menu->Settings.<br>
Name the new project. Select a directory where STMCube can create subfolders to store project files.<br>
Change the Toolchain/IDE dropdown menu to MDK-ARM V5.<br>
On the Project tab, move to the Code Generator tab at the top of the window.<br>
STMCube may take a while to copy the files to the directory specified in the settings. Afterward,
you may be asked if you want to open the project folder or project file itself. Click "project file".<br>
Now you should be in the "Keil uVision5" program as it's opened automatically.<br><br>

Keil uVision5:<br>

Click "Flash" -> "Configure flash tools" from the top menu.<br>
Click "Target" from the top menu. Find "Arm complier" menu and select 
"use default compiler version..".


One the setting is done, replace the main.c file in the "Application/User/Core" folder <br>
with my main.c file you downloaded.<br>
From the top menu, "Project"->"Build Target".<br>
Plug in your STM32F072 Discovery Microcontroller to your computer. <br>
Click "Flash" -> "Download" from the top menu. Test it on your STM32F072 Discovery Microcontroller.

Thank you for evaluating this project and providing feedback. <br>

Have a wonderful day!

# Consulted Peers:
N/A

# Caution/Warnings
* This lab involves wiring systems with different operating voltages together! You MUST be careful how you connect things, or you will damage either your board or the motor encoder. Read the lab—as well as the comments in the template project—carefully!

* Although Kiel μVision generates ELF-type files for programming the STM32F0, it saves them in the project directory with an .AXF file extension. This file can be found in the “<project folder>/MDK-ARM/<project name>/” directory. Make a copy and rename the file extension to .ELF for use with STMStudio.

* Be careful not to connect the motor connector backwards! If you do, you’ll reverse power and ground on the quadrature encoder. Most devices aren’t designed for this condition and you’ll likely fry it.




# Examples of Good Software Practice (GSP)
<pre><ins>DRY</ins> :</pre>
DRY is an abbreviation of "Don't repeat yourself". It's a principle of Software Engineering that
has the goal of reducing repetition and redundancy in the coding. Using abstractions and normalization
are advised over redundancy <a href="https://en.wikipedia.org/wiki/Don%27t_repeat_yourself">[2]</a>.

<pre><ins>Separation of Concerns</ins> :</pre>
This concept is similar to the "divide and conquer" principle where you divide
a big software project into small projects to complete. A software design technique that focuses on separating 
and freeing functionalities of a program is called Modular programming. Making each of the divided small 
projects independent and addressing a separate concern, it'll make it easy to reduce, detect 
and fix the errors. <a href="https://en.wikipedia.org/wiki/Separation_of_concerns">[3]</a>

<pre><ins>Good Code Typing Practices</ins> :</pre>
Good coding practices can be listed as: Naming variables with a relevant name, commenting 
in between code lines with a brief explanation if the code is not self-explanatory, creating 
helper methods that can be used multiple times and by other sections.


<pre><ins>Testing Strategies</ins> :</pre>
Unit Testing can be summarized in 3 types of techniques:<br>

1. <ins>Black Box Testing : </ins> In this testing, input, user interface, and output parts are covered.
2. <ins>White Box Testing : </ins> In this testing, functionality, design structure, and code models are covered.
3. <ins>Gray Box Testing : </ins> In this testing, analysis of code performance, relevant test cases,
methods, and functions are covered.<a href="https://www.geeksforgeeks.org/unit-testing-software-testing/">[4]</a>


# References:
1. Canvas Page Class Materials.(For example, lecture slides, additional resources and pdf files). <br>
2. https://en.wikipedia.org/wiki/Don%27t_repeat_yourself<br>
3. https://en.wikipedia.org/wiki/Separation_of_concerns<br>
4. https://www.geeksforgeeks.org/unit-testing-software-testing/<br>






